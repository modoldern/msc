<script>
  import Carousel from "../components/LinkCard.svelte";
  import linksData from "../json/links-data.json"; // JSON dosyasını import et
  let links = linksData.links; // JSON'daki 'links' dizisini al
</script>

<h2 class="text-4xl font-bold mt-16 mb-4">{linksData.title}</h2>
<Carousel autoplay={2000} onChange>
  {#each links as { title, image }, index (index)}
    <div class="w-1/2 md:w-1/4">
      <img
        src={image}
        alt={title}
        style="width: 100%; height: 100%; object-fit: cover;"
      />
      <h3>{title}</h3>
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
  h3 {
    margin-top: 0.5rem;
    text-align: center;
    font-size: 1rem;
    font-weight: bold;
  }
</style>
