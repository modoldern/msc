<script>
  export let title;
  export let date;
  export let image;


  $: formatteYear = new Date(date * 1000).toLocaleDateString("en-US", {
    year: "numeric",
  });
  $: formatteMonth = new Date(date * 1000).toLocaleDateString("en-US", {
    month: "short",
  });
  $: formatteDay = new Date(date * 1000).toLocaleDateString("en-US", {
    day: "numeric",
  });
</script>

<div class="bg-msclight overflow-hidden transition-shadow shadow-xl hover:shadow-md h-full">
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
  </div>
</div>
