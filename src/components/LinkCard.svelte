<script>
  import Siema from "siema";
  import { onMount, onDestroy } from "svelte";

  export let perPage = { default: 2, md: 4, xl: 6 };
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
  let currentPerPage = perPage.default;

  function updatePerPage() {
    if (window.matchMedia("(min-width: 1280px)").matches) {
      currentPerPage = perPage.xl;
    } else if (window.matchMedia("(min-width: 768px)").matches) {
      currentPerPage = perPage.md;
    } else {
      currentPerPage = perPage.default;
    }

    if (controller) {
      controller.perPage = currentPerPage;
      if (typeof onChange === "function") { 
        controller.update()
      }
    }
  }

  onMount(() => {
    updatePerPage();
    window.addEventListener("resize", updatePerPage);

    controller = new Siema({
      selector: siema,
      perPage: currentPerPage,
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

    return () => {
      autoplay && clearInterval(timer);
      controller.destroy();
      window.removeEventListener("resize", updatePerPage);
    };
  });

  onDestroy(() => {
    window.removeEventListener("resize", updatePerPage);
  });

  export function left() {
    controller.prev();
  }

  export function right() {
    controller.next();
  }

  export function go(index) {
    controller.goTo(index);
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
    currentIndex = controller.currentSlide;
    if (typeof onChange === "function") {
      onChange({
        currentSlide: controller.currentSlide,
        slideCount: controller.innerElements.length,
      });
    }
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
