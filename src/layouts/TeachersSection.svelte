<script>
  import TeacherCard from '../components/PersonCard.svelte';
  import teachersData from '../json/teachers-data.json';
  import { writable } from 'svelte/store';
 import { onMount } from 'svelte';

  // Aktif sayfa indeksi için store
  const activeIndex = writable(0);
  let visibleCards = 4; // Default: md ve üzeri için 4 kart

  // Responsive visibleCards ayarlaması
  onMount(() => {
    const updateVisibleCards = () => {
      const width = window.innerWidth;
      if (width < 640) {
        // xs ekran: w-full yani 1 kart
        visibleCards = 1;
      } else if (width < 768) {
        // sm ekran: sm:w-1/2 yani 2 kart
        visibleCards = 2;
      } else {
        // md ve üzeri: md:w-1/4 yani 4 kart
        visibleCards = 4;
      }
    };

    // İlk kontrol
    updateVisibleCards();
    // Dinamik olarak ekran boyutu değiştiğinde güncelle
    window.addEventListener('resize', updateVisibleCards);
    return () => window.removeEventListener('resize', updateVisibleCards);
  });
  
  // Son sayfadaki eksik kart sayısını hesapla
  $: remainingCards = teachersData.teachers.length % visibleCards;
  $: totalPages = Math.ceil(teachersData.teachers.length / visibleCards);
  
  // Son sayfada kaydırma miktarını ayarla
  $: translateX = $activeIndex === totalPages - 1 && remainingCards !== 0
    ? -((teachersData.teachers.length - visibleCards) * 100 / visibleCards) + '%'
    : -($activeIndex * 100) + '%';
  
  function next() {
    $activeIndex = Math.min($activeIndex + 1, totalPages - 1);
  }
  
  function prev() {
    $activeIndex = Math.max($activeIndex - 1, 0);
  }

  $: canGoNext = $activeIndex < totalPages - 1;
  $: canGoPrev = $activeIndex > 0;
</script>

<section class="py-16 bg-msclight w-full px-5 xl:px-0">
  <div class="">
    <div class="text-center mb-12 break-all">
      <h2 class="text-4xl font-bold mb-4">{teachersData.title}</h2>
      <p class="text-gray-600 max-w-2xl mx-auto">
        {teachersData.description}
      </p>
    </div>

    <div class="relative">
      {#if canGoPrev}
        <button aria-label="prev"
          on:click={prev}
          class="absolute left-0 top-1/2 -translate-y-1/2 translate-x-12 z-10 bg-white rounded-full p-3 shadow-lg hover:bg-gray-100 transition-colors cursor-pointer"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 19l-7-7 7-7"
            />
          </svg>
        </button>
      {/if}

      {#if canGoNext}
        <button aria-label="next"
          on:click={next}
          class="absolute right-0 top-1/2 -translate-y-1/2 -translate-x-12 z-10 bg-white rounded-full p-3 shadow-lg hover:bg-gray-100 transition-colors cursor-pointer"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 5l7 7-7 7"
            />
          </svg>
        </button>
      {/if}

      <div class="overflow-hidden">
        <div
          class="flex transition-transform duration-300 ease-in-out"
          style="transform: translateX({translateX})"
        >
          {#each teachersData.teachers as teacher}
            <div class="w-full sm:w-1/2 md:w-1/4 flex-shrink-0 px-4">
              <TeacherCard {teacher} />
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>

<style>

</style>