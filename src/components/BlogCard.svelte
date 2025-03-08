<script>
  export let title;
  export let date;
  export let image;
  export let content;

  $: truncatedContent =
    content.length > 200 ? content.slice(0, 200) + "..." : content;

  $: formatteYear = new Date(date).toLocaleDateString("en-US", {
    year: "numeric",
  });
  $: formatteMonth = new Date(date).toLocaleDateString("en-US", {
    month: "short",
  });
  $: formatteDay = new Date(date).toLocaleDateString("en-US", {
    day: "numeric",
  });
</script>

<div class="bg-msclight overflow-hidden shadow-lg group">
  <div class="relative">
    <img
      src={image}
      alt={title}
      class="w-full h-full aspect-[4/3] object-cover object-top"
    />
    <div
      class="flex flex-col items-start absolute bottom-0 left-0 bg-mscsecondary-02/60 text-white px-2 py-3 text-base"
    >
      <span class="text-2xl font-bold">{formatteDay}</span>
      <span>{formatteMonth}</span>
      <span>{formatteYear}</span>
    </div>
  </div>
  <div class="p-6 flex flex-col items-start text-left">
    <h2 class="text-xl font-semibold text-gray-900 mb-4">{title}</h2>
    <p class="text-gray-600 mb-6 leading-relaxed">{truncatedContent}</p>
    <button
      class="bg-mscprimary hover:bg-mscsecondary-01 cursor-pointer text-white px-4 py-2 font-medium group-hover:translate-x-0.5 transition-colors duration-200"
    >
      Daha Fazla
    </button>
  </div>
</div>
