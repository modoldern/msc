<script>
  import BlogCard from "../components/BlogCard.svelte";
  import blogData from "../json/blog-data.json";
  import { Link } from "svelte-routing";
  const { posts } = blogData;
  export let blogPosts = posts;

</script>

<div
  class="w-full flex flex-col items-center gap-20 px-5 py-20 xl:px-0 xl:w-6xl"
>
  <h1 class="font-bold text-3xl text-mscdark">სიახლეები</h1>
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-8 gap-y-14">
    {#each blogPosts as item (item.id)}
    <Link to="/blog/{item.id}/{item.slug}">
      <BlogCard
        title={item.title}
        date={item.date}
        image={item.image}
      />
      </Link>
    {/each}
    
  </div>
</div>
