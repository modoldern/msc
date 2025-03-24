<script>
  import { faYammer } from "@fortawesome/free-brands-svg-icons";
  export let id;
  let blogPost;
  import blogData from "../json/blog-data.json";
  import RecentNews from "../layouts/RecentNews.svelte";
  import { Link, Router } from "svelte-routing";
  let months = [
    "იანვარი",
    "თებერვალი",
    "მარტი",
    "აპრილი",
    "მაისი",
    "ივნისი",
    "ივლისი",
    "აგვისტო",
    "სექტემბერი",
    "ოქტომბერი",
    "ნოემბერი",
    "დეკემბერი",
  ];
  const { posts } = blogData;
  // Bu kod, URL'deki slug'ı alarak uygun postu buluyor
  import { onMount } from "svelte";
  $: lastPosts = posts.slice(-5);
  const blogPosts = posts;
  $: {
    blogPost = blogPosts.find((post) => post.id === parseInt(id));
    if (!blogPost) {
      blogPost = { content: "Bu haber bulunamadı." };
    }
  }
  onMount(() => {
    window.scrollTo(0, 0);
  });
</script>

<div class="w-full flex flex-col md:flex-row items-start gap-30 md:gap-10 px-5 py-20 xl:px-0 xl:w-6xl">
  <main class="flex flex-col gap-12 xl:w-6xl">
    {#if blogPost}
      <!-- Resim ve Tarih -->

      <div class="relative">
        <img src={blogPost.image} alt="Haber Resmi" class="w-full h-auto" />

        <div
          class="flex flex-col items-start absolute bottom-0 left-0 bg-mscsecondary-02/60 text-white px-2 py-3 text-base"
        >
          <span class="text-2xl font-bold"
            >{`${new Date(blogPost.date).getDate()}`}</span
          ><span
            >{`${months[new Date(blogPost.date).getMonth()].slice(0, 3)}`}</span
          ><span>{`${new Date(blogPost.date).getFullYear()}`}</span>
        </div>
      </div>
      <h1 class="text-left font-bold text-4xl">{blogPost.title}</h1>
      <!-- Haber Metni -->
      <div class="bg-[var(--color-msclight)] text-left">
        <p class="leading-8">{blogPost.content}</p>
      </div>
    {:else}
      <p>Haber bulunamadı.</p>
    {/if}
  </main>

  <RecentNews {blogData} />
</div>
