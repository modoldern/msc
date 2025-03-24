<script>
  import Carousel from "../components/LinkCard.svelte";
  import linksData from "../json/links-data.json";
  let links = linksData.links;
</script>

<h2 class="text-3xl font-bold mt-16 mb-4">{linksData.title}</h2>
<Carousel autoplay={2000} onChange >
  {#each links as { title, image }, index (index)}
    <div class="w-1/2 md:w-1/4">
      <img
        src={image}
        alt={title}
        class="w-16 sm:w-full h-full object-cover mb-3"
      />
      <span class="text-xs sm:text-base font-bold">{title}</span>
    </div>
  {/each}
</Carousel>

<style>
  div {
    height: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    margin: 0 auto;
  }
  img {
    height: auto;
  }
  span {
    margin-top: 0.5rem;
    text-align: center;
    font-size: 1rem;
    font-weight: bold;
  }
</style>
