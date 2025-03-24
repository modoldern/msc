<script>
  export let blogData;
  import RecentNewsCard from "../components/RecentNewsCard.svelte";
  import { Link, Router } from "svelte-routing";
  const { posts } = blogData;
  $: lastPosts = posts.slice(-4);
  const blogPosts = posts;
</script>

<aside class="w-auto bg-amber-500">
  <div class="bg-[var(--color-msclight)]">
    <h2 class="text-left text-xl font-bold mb-4">ბოლო სიახლეები</h2>
    <div class="flex flex-col gap-4 sm:gap-10 md:gap-0">
      <Router>
        {#each lastPosts as post (post.id)}
          <Link to="/blog/{post.id}/{post.slug}">
            <RecentNewsCard
              image={post.image}
              content={post.content}
              date={post.date}
            />
          </Link>
        {/each}
      </Router>
    </div>
  </div>
</aside>
