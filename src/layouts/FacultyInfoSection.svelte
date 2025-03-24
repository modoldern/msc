<script>
  // json
  import sliderDataJson from "../json/slider-data.json";
  import contentData from "../json/content-data.json";
  const { contents } = contentData;


  import Slider from "../components/Slider.svelte";
  import DataCard from "../components/FacultyInfoCard.svelte";
</script>

<Slider slides={sliderDataJson.slides} />
<div class="grid sm:grid-cols-2 lg:grid-cols-4 min-w-full">
  {#each contents as { icon, title, description, author }, index}
    <DataCard {icon} {title} {description} {author} {index} />
  {/each}
</div>
