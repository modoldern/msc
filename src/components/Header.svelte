<script>
  export let headerData;
</script>

<div class="w-full flex flex-col sm:flex-row sm:justify-between gap-3 sm:gap-0 p-4 xl:p-0 items-center sm:h-26">
  <img src={headerData.logo} alt="logo" class="h-20 w-20" />
  <div>
    <ul class="flex flex-col sm:flex-row justify-between sm:items-center sm:gap-3">
      {#each headerData.contacts as contact}
        <li class="flex items-center gap-1">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="1rem"
            viewBox={contact.icon.viewBox}
            fill="var(--color-mscprimary)"
          >
            <path d={contact.icon.path} />
          </svg>
          <span class="text-[1rem]">{contact.value}</span>
        </li>
      {/each}
    </ul>
  </div>
</div>