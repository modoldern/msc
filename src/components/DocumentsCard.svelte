<script>
    export let pdfFiles;
    export let head;
</script>
<main class="flex flex-col gap-3 w-full">
    <h1 class="text-xl font-bold text-gray-800 mb-4 text-left">
      {head}
    </h1>
    <div class="flex items-center text-gray-600 text-sm mb-4 gap-3">
      <span>ბოლო განახლება:</span> <span class="mr-2">05-მარტი-2024</span>
    </div>

    <div class="space-y-2">
      {#if pdfFiles.length > 0}
        {#each pdfFiles as pdf}
          <a
            href={pdf.path}
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center text-left gap-2 bg-gray-100 hover:bg-gray-200 p-3"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              height="24px"
              viewBox="0 -960 960 960"
              width="24px"
              fill="#0099D1"
              ><path
                d="M320-240h320v-80H320v80Zm0-160h320v-80H320v80ZM240-80q-33 0-56.5-23.5T160-160v-640q0-33 23.5-56.5T240-880h320l240 240v480q0 33-23.5 56.5T720-80H240Zm280-520v-200H240v640h480v-440H520ZM240-800v200-200 640-640Z"
              /></svg
            >{pdf.name}
          </a>
        {/each}
      {:else}
        <p>გვერდი არ არსებობს</p>
      {/if}
    </div>
  </main>
