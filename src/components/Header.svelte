<script>
  // json
  import headerDataJson from "../json/header-data.json";
  //   components
  import NavMenu from "../components/NavMenu.svelte";
  import HeaderBranding from "../components/HeaderBranding.svelte";
  import { Router, Link, Route } from "svelte-routing";
</script>

<header
  class="w-full xl:w-6xl h-auto lg:h-44 flex flex-col items-start xl:items-stretch justify-between relative z-20"
>
  <HeaderBranding headerData={headerDataJson} />
  <div
    class="nav w-full p-4 lg:p-0 gap-4 lg:gap-0 lg:h-18 bg-mscsecondary-01 flex flex-col-reverse items-start lg:flex-row lg:items-center lg:justify-between lg:px-5 text-msclight"
  >
    <NavMenu />
    <div class="w-full sm:w-auto">
      <input
        type="text"
        placeholder="ძიება"
        class="border-msclight w-full sm:w-auto border p-2 rounded-4xl outline-0"
      />
    </div>
    
  </div>
</header>
