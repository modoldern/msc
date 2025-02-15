<script>
  let title = "გამარჯობა";
  // json
  import headerDataJson from "./json/header-data.json";
  import menuDataJson from "./json/menu-data.json";
  import sliderDataJson from "./json/slider-data.json";
  import contentData from "./json/content-data.json";
  const { contents } = contentData;
  import offerData from "./json/offer-data.json";
  import universityData from "./json/university-data.json";

  // components
  import Menu from "./components/Menu.svelte";
  import Slider from "./components/Slider.svelte";
  import DataCard from "./components/DataCard.svelte";
  import Header from "./components/Header.svelte";
  import WhatWeOffer from "./components/Offer.svelte";
  import UniversityHero from "./components/UniversityHero.svelte";
  import TeachersSection from "./layouts/TeachersSection.svelte";
  import Footer from "./layouts/Footer.svelte";
  import { footerData } from "./json/footer-data.json";

  import { fly, slide, blur, fade, scale } from "svelte/transition";
</script>

<main
  class="text-center py-0 min-h-screen flex flex-col items-center font-georgian"
>
  <header
    class="w-full xl:w-6xl h-44 flex flex-col items-start xl:items-stretch justify-between relative z-20"
  >
    <Header headerData={headerDataJson} />
    <div
      class="nav w-full p-4 lg:p-0 gap-4 lg:gap-0 lg:h-18 bg-mscsecondary-01 flex flex-col-reverse items-start lg:flex-row lg:items-center lg:justify-between lg:px-5 text-msclight"
    >
      <Menu />
      <div class="w-full sm:w-auto">
        <input
          type="text"
          placeholder="ძიება"
          class="border-msclight w-full sm:w-auto border p-2 rounded-4xl outline-0"
        />
      </div>
    </div>
  </header>
  <Slider slides={sliderDataJson.slides} />
  <div class="grid sm:grid-cols-2 lg:grid-cols-4 min-w-full">
    {#each contents as { icon, title, description, author }, index}
      <DataCard {icon} {title} {description} {author} {index} />
    {/each}
  </div>

  <WhatWeOffer {offerData} />
  <UniversityHero {universityData} />
  <TeachersSection />
  <Footer {footerData} />
</main>

<style>
</style>
