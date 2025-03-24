<script>
  import { onMount } from "svelte";
  import blogData from "../json/blog-data.json";
  import RecentNews from "../layouts/RecentNews.svelte";
  import DocumentsCard from "../components/DocumentsCard.svelte";
  let fileName = import.meta.url.split("/").pop().split(".")[0].toLowerCase();
  const { posts } = blogData;
  let pdfFiles = [];
  let isLoading = false;
  let error = null;
  async function fetchPdfs() {
    isLoading = true;
    error = null;
    try {
      const response = await fetch(`/docs/${fileName}/${fileName}.json`);
      if (!response.ok) {
        throw new Error("Dosyalar alınamadı");
      }
      const files = await response.json();
      pdfFiles = files.map((file) => ({
        name: file,
        path: `/docs/${fileName}/${file}`,
      }));
    } catch (err) {
      error = err.message;
    } finally {
      isLoading = false;
    }
  }
  fetchPdfs();
  onMount(() => {
    window.scrollTo(0, 0);
  });
</script>

<div class="w-full flex flex-col md:flex-row items-start gap-30 md:gap-10 px-5 py-20 xl:px-0 xl:w-6xl">
  <DocumentsCard head={"გზამკვლევი აპლიკანტებს"} {pdfFiles} />
  <RecentNews {blogData} />
</div>
