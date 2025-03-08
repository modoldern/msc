<script>
  import { onMount } from "svelte";
  import headerDataJson from "../json/header-data.json"
  export let slides = [];
  import { fade, slide, fly, scale } from "svelte/transition";
  let visible = false;

  // Sayfa yüklendiğinde animasyonu tetikle
  onMount(() => {
    visible = true;
  });
  let currentSlide = 0;
  let intervalId;

  function nextSlide() {
    currentSlide = (currentSlide + 1) % slides.length;
  }

  function prevSlide() {
    currentSlide = (currentSlide - 1 + slides.length) % slides.length;
  }

  function goToSlide(index) {
    currentSlide = index;
  }

  onMount(() => {
    intervalId = setInterval(nextSlide, 5000);
    return () => clearInterval(intervalId);
  });
</script>

<div transition:fly={{ y: 10, duration: 300 }} class="slider w-full h-[600px] relative overflow-hidden flex justify-center">
  {#each slides as slide, index}
    <div 
      class="slide w-full h-full absolute bg-cover bg-center transition-opacity opacity-0 ease-in-out duration-500"
      class:active={index === currentSlide}
      style="background-image: url({slide.src})"
    >
      <div class="overlay w-full h-full bg-[var(--alfa-mscsecondary-01)] absolute top-0 left-0"></div>
    </div>
  {/each}

  <div class="dots flex gap-2.5 absolute bottom-5 left-[50%] translate-x-[-50%]">
    {#each slides as slide, index}
      <button
        class="dot w-3 h-3 bg-msclight rounded-full border-none cursor-pointer transition-[color] duration-300"
        class:active={index === currentSlide}
        on:click={() => goToSlide(index)}
        aria-label="Go to slide {index + 1}: {slide.title}"
      ></button>
    {/each}
  </div>
  <div transition:fly={{ y: -50, duration: 300 }} class="flex items-baseline flex-col justify-start gap-5 w-full px-5 xl:px-0 xl:w-6xl my-0 relative top-40 break-all">
    <div class="notice text-4xl leading-13 sm:text-6xl sm:leading-20 text-left font-bold text-msclight">სწავლასთან <br /> დაკავშირებით</div>
    <a class="bg-mscprimary rounded-3xl p-3 text-msclight" href="tel:{headerDataJson.contacts.filter(e => e.type === "phone")[0].value}">დაგვირეკეთ</a>
  </div>
</div>

<style>

  .slide.active {
    opacity: 1;
  }
  .dot.active {
    background-color: var(--color-mscprimary);
  }
</style>
