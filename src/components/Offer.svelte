<script>
  export let offerData;
  import { onMount } from "svelte";
  import { fade, slide, fly, scale } from "svelte/transition";
  let visible = false;

  // Sayfa yüklendiğinde animasyonu tetikle
  onMount(() => {
    visible = true;
  });
  
</script>

<div transition:fly={{ y: 10, duration: 300 }} class="flex w-full px-5 xl:px-0 xl:w-6xl min-h-[930px]">
  <div class="flex flex-col py-8 gap-14 justify-center h-full md:pr-8">
    <div class="flex flex-col gap-8">
      <h2 class="text-3xl font-semibold text-left">{offerData.title}</h2>
      <p class="text-mscaccentdark text-sm sm:text-base text-left">{offerData.description}</p>
    </div>

    <div class="grid lg:grid-cols-2 lg:gap-x-6 gap-y-16">
      {#each offerData.offers as offer}
        <div class="flex items-start ">
          <div
            class="w-15 h-15 sm:w-20 sm:h-20 bg-mscprimary rounded-full flex items-center justify-center flex-shrink-0"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              height="2rem"
              viewBox={offer.icon.viewBox}
              fill="var(--color-msclight)"
            >
              <path d={offer.icon.path} />
            </svg>
          </div>
          <div class="ml-4 break-all">
            <h3 class="font-semibold sm:text-lg mb-2 text-left">{offer.title}</h3>
            <p class="text-mscaccentdark text-sm sm:text-base text-left">{offer.description}</p>
          </div>
        </div>
      {/each}
    </div>
  </div>

  <div class="w-full hidden md:block">
    <img
      src={offerData.image}
      alt="Students"
      class="w-full h-full object-cover"
    />
  </div>
</div>
