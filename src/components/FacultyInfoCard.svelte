<script>
  export let icon;
  export let title;
  export let description;
  export let index;
  export let author;
</script>

<div
  class={`${index % 2 === 0 ? "lg:bg-[var(--color-mscprimary)] bg-[var(--color-mscprimary)]" : "lg:bg-[var(--color-mscsecondary-01)] bg-[var(--color-mscsecondary-01)]"} ${index===0 || index===3 ? "sm:bg-[var(--color-mscprimary)]" : "sm:bg-[var(--color-mscsecondary-01)]"} min-h-[310px] sm:pt-12 flex flex-col px-3 items-center justify-center sm:justify-baseline gap-4 text-msclight`}
>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    height="4rem"
    viewBox={icon.viewBox}
    fill="var(--color-msclight)"
  >
    <path d={icon.path} />
  </svg>
  <h2 class="text-2xl font-bold">{title}</h2>
  <div>
    <p class="italic">"{description}"</p>
    <span>{author}</span>
  </div>
</div>

<style>

</style>
