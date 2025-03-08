<script>
  import BlogCard from "../components/BlogCard.svelte";
  import blogData from "../json/blog-data.json";

  const { posts } = blogData;
</script>

<div
  class="w-full flex flex-col items-center gap-20 px-5 py-20 xl:px-0 xl:w-6xl"
>
  <h1 class="font-bold text-3xl text-mscdark">სიახეები</h1>
  <div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-8">
    {#each posts as post (post.id)}
      <BlogCard
        title={post.title}
        date={post.date}
        image={post.image}
        content={post.content}
      />
    {/each}
  </div>
</div>
