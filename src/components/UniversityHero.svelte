<script>
  export let universityData;
</script>

<div class="relative w-full py-12 md:py-0 min-h-[785px] flex justify-center overflow-hidden">
  <!-- Arkaplan Resmi ve Overlay -->
  <div class="absolute inset-0">
    <img
      src={universityData.backgroundImage}
      alt="Background"
      class="w-full h-full object-cover"
    />
    <div class="absolute inset-0 bg-[var(--alfa-mscsecondary-01)]"></div>
  </div>

  <div class="relative w-2xl xl:w-6xl px-5 xl:px-0">
    <div class="flex flex-col h-full items-center justify-center gap-5 md:gap-17">
      <!-- Video ve İçerik -->
      <div class="flex flex-col md:flex-row items-center justify-between w-full gap-12 md:gap-8">
        <!-- Sol Taraf - Video -->
        <div class="w-full md:w-84 xl:w-xl">
          <div class="bg-msclight rounded-lg overflow-hidden shadow-xl">
            <div class="relative max-md:pb-[56.25%] md:pb-[130%] xl:pb-[56.25%] w-full">
              <iframe
                title={universityData.title}
                src={`https://www.youtube.com/embed/${universityData.youtubeVideoId}`}
                class="absolute top-0 left-0 w-full h-full"
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen
              ></iframe>
            </div>
          </div>
        </div>

        <!-- Sağ Taraf - İçerik -->
        <div class="w-full md:w-84 xl:w-xl flex flex-col gap-3 xl:gap-8 text-msclight text-left">
          <h1 class=" text-3xl md:text-3xl xl:text-5xl font-bold break-all">{universityData.title}</h1>
          <p class="xl:text-lg">{universityData.description}</p>
          <p class="">{universityData.shortDescription}</p>
        </div>
      </div>

      <!-- İstatistikler -->
      <div class="grid md:grid-cols-4 gap-15 md:gap-20 w-full">
        {#each universityData.stats as stat}
          <div class="text-center text-msclight">
            <div class="text-5xl font-bold mb-2">{stat.number}</div>
            <div class="text-sm">{stat.label}</div>
          </div>
        {/each}
      </div>
    </div>
  </div>
</div>