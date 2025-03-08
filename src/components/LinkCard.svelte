<script>
  import Siema from "siema";
  import { onMount } from "svelte";

  export let perPage = { xs: 3, md: 6 }; // Default as an object with breakpoints
  export let loop = true;
  export let autoplay = 0;
  export let duration = 200;
  export let easing = "ease-out";
  export let startIndex = 0;
  export let draggable = true;
  export let multipleDrag = true;
  export let threshold = 20;
  export let rtl = false;

  export let onChange;

  let currentIndex = startIndex;
  let siema;
  let controller;
  let timer;
  let currentBreakpoint = "";
  let resizeTimeout;

  $: pips = controller ? controller.innerElements : [];
  $: currentPerPage = getCurrentPerPage();
  $: totalDots = controller
    ? Math.ceil(controller.innerElements.length / currentPerPage)
    : [];

  function getCurrentPerPage() {
    if (!controller) return perPage.xs;
    return controller.perPage;
  }

  function getCurrentBreakpoint() {
    const width = window.innerWidth;
    return width >= 768 ? "md" : "xs";
  }

  // Debounced resize handler
  function handleResize() {
    clearTimeout(resizeTimeout);
    resizeTimeout = setTimeout(() => {
      const newBreakpoint = getCurrentBreakpoint();

      // Only update if breakpoint changed
      if (newBreakpoint !== currentBreakpoint) {
        currentBreakpoint = newBreakpoint;
        const newPerPage = perPage[currentBreakpoint];

        // Store current slide
        const currentSlide = controller ? controller.currentSlide : 0;

        // Destroy and recreate with new perPage
        if (controller) {
          controller.destroy();
        }

        controller = new Siema({
          selector: siema,
          perPage: newPerPage,
          loop,
          duration,
          easing,
          startIndex: currentSlide, // Preserve position
          draggable,
          multipleDrag,
          threshold,
          rtl,
          onChange: handleChange,
        });

        // Update any UI that depends on controller
        onChange?.({
          currentSlide: controller.currentSlide,
          slideCount: controller.innerElements.length,
        });
      }
    }, 150); // Debounce time
  }

  onMount(() => {
    // Set initial breakpoint
    currentBreakpoint = getCurrentBreakpoint();

    // Initialize carousel
    controller = new Siema({
      selector: siema,
      perPage: perPage[currentBreakpoint],
      loop,
      duration,
      easing,
      startIndex,
      draggable,
      multipleDrag,
      threshold,
      rtl,
      onChange: handleChange,
    });

    if (autoplay) {
      timer = setInterval(right, autoplay);
    }

    // Add resize event listener with debouncing
    window.addEventListener("resize", handleResize);

    return () => {
      autoplay && clearInterval(timer);
      clearTimeout(resizeTimeout);
      window.removeEventListener("resize", handleResize);
      if (controller) controller.destroy();
    };
  });

  export function isDotActive(currentIndex, dotIndex) {
    if (currentIndex < 0) currentIndex = pips.length + currentIndex;
    return (
      currentIndex >= dotIndex * currentPerPage &&
      currentIndex < dotIndex * currentPerPage + currentPerPage
    );
  }

  export function left() {
    controller && controller.prev();
  }

  export function right() {
    controller && controller.next();
  }

  export function go(index) {
    controller && controller.goTo(index);
  }

  export function pause() {
    clearInterval(timer);
  }

  export function resume() {
    if (autoplay) {
      timer = setInterval(right, autoplay);
    }
  }

  function handleChange(event) {
    if (!controller) return;
    currentIndex = controller.currentSlide;

    onChange?.({
      currentSlide: controller.currentSlide,
      slideCount: controller.innerElements.length,
    });
  }
</script>

<div class="carousel py-16">
  <div class="slides" bind:this={siema}>
    <slot></slot>
  </div>
</div>

<style>
  .carousel {
    position: relative;
    width: 100%;
  }
</style>
