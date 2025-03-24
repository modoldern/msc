<script>
  import { fade, slide, fly, scale } from "svelte/transition";
  import { onMount, onDestroy } from "svelte";
  import { Link, Router } from "svelte-routing";

  let visible = false;
  let activeMenu = null;
  let activeSubmenu = null;
  let isOpen = false;

  // Sayfa yüklendiğinde animasyonu tetikle
  onMount(() => {
    visible = true;

    // Document click listener ekle
    document.addEventListener("click", handleOutsideClick);
  });

  // Component yok edildiğinde listener'ı kaldır
  onDestroy(() => {
    document.removeEventListener("click", handleOutsideClick);
  });

  // Menü tıklamalarını kontrol eden fonksiyon
  const handleMenuClick = (menuId) => {
    if (activeMenu === menuId) {
      activeMenu = null;
      activeSubmenu = null;
    } else {
      activeMenu = menuId;
      activeSubmenu = null;
    }
  };

  const handleSubmenuClick = (submenuId) => {
    if (activeSubmenu === submenuId) {
      activeSubmenu = null;
    } else {
      activeSubmenu = submenuId;
    }
  };

  // Menü dışında bir yere tıklanırsa menüyü kapat
  const handleOutsideClick = (event) => {
    const dropdown = document.querySelector("nav");
    if (dropdown && !dropdown.contains(event.target)) {
      activeMenu = null;
      activeSubmenu = null;
      isOpen = false;
    }
  };
  const closeMenu = () => {
    activeMenu = null;
    activeSubmenu = null;
    isOpen = false;
  };
</script>

<Router>
  <nav class="text-msclight lg:h-44 w-full lg:flex">
    <div class="flex flex-wrap justify-between items-center">
      <button
        aria-label="btn"
        on:click={() => (isOpen = !isOpen)}
        class="lg:hidden p-2 focus:outline-none {isOpen
          ? 'scale-120'
          : 'scale-100'} transition-transform"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          stroke-width="2"
          class="text-msclight"
        >
          <path
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M4 6h16M4 12h16M4 18h16"
          />
        </svg>
      </button>

      <div
        class="w-full lg:block lg:w-auto {isOpen ? 'block' : 'hidden'}"
        transition:fly={{ y: 10, duration: 200 }}
      >
        <ul
          transition:fly={{ y: 10, duration: 300 }}
          class="flex flex-col items-start lg:flex-row lg:mt-0 text-sm font-medium"
        >
          <!-- Home -->
          <li>
            <Link
              to="/"
              class="block py-2 px-2 hover:text-mscsecondary-02"
              on:click={closeMenu}>მთავარი</Link
            >
          </li>

          <!-- About Us -->
          <li class="relative">
            <button
              on:click={() => handleMenuClick("about")}
              class="cursor-pointer py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
            >
              ჩვენს შესახებ
              <svg
                class="w-4 h-4 ml-2"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19 9l-7 7-7-7"
                />
              </svg>
            </button>

            {#if activeMenu === "about"}
              <ul
                class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max lg:whitespace-nowrap flex-col items-center"
                transition:fly={{ y: 10, duration: 400 }}
              >
                <li class="border-b">
                  <Link
                    to="/struqtura"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    სტრუქტურა
                  </Link>
                </li>

                <!-- Teachers submenu -->
                <li class="relative border-b">
                  <button
                    on:click={() =>
                      handleSubmenuClick("vocational-education-teachers")}
                    class="cursor-pointer p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
                  >
                    პროფესიული განათლების მასწავლებლები
                    <svg
                      class="w-4 h-4 ml-2"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M19 9l-7 7-7-7"
                      />
                    </svg>
                  </button>

                  {#if activeSubmenu === "vocational-education-teachers"}
                    <ul
                      class="lg:absolute text-left lg:left-full lg:top-0 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full whitespace-normal flex-col items-center"
                      transition:fly={{ x: -10, duration: 400 }}
                    >
                      <li class="border-b">
                        <Link
                          to="/profesiuli-ganatlebis-mastsavleblisprogramis-ganmakhorcieleblis-samsakhurshi-mighebis-tsesi"
                          class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                          on:click={closeMenu}
                        >
                          პროფესიული განათლების მასწავლებლის/პროგრამის
                          განმახორციელებლის სამსახურში მიღების წესი
                        </Link>
                      </li>
                      <li>
                        <Link
                          to="/profesiuli-mastsavleblis-gzamkvlevebi"
                          class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                          on:click={closeMenu}
                        >
                          პროფესიული მასწავლებლის გზამკვლევები
                        </Link>
                      </li>
                    </ul>
                  {/if}
                </li>
                <!-- Other menu items -->
                <li class="border-b">
                  <Link
                    to="/samoqmedo-gegmebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    სამოქმედო გეგმები
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/maregulirebeli-aqtebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    მარეგულირებელი აქტები
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/avtorizaciis-gadatsyvetileba"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    ავტორიზაციის გადაწყვეტილება
                  </Link>
                </li>
                <!-- Personnel -->
                <li class="relative border-b">
                  <button
                    on:click={() => handleSubmenuClick("personnel")}
                    class="cursor-pointer p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
                  >
                    პერსონალი
                    <svg
                      class="w-4 h-4 ml-2"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M19 9l-7 7-7-7"
                      />
                    </svg>
                  </button>

                  {#if activeSubmenu === "personnel"}
                    <ul
                      class="lg:absolute text-left lg:left-full lg:top-0 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
                      transition:fly={{ x: -10, duration: 400 }}
                    >
                      <li class="border-b">
                        <Link
                          to="/administracia"
                          class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                          on:click={closeMenu}
                        >
                          ადმინისტრაცია
                        </Link>
                      </li>
                      <li>
                        <Link
                          to="/profesiuli-mastsavleblebi"
                          class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                          on:click={closeMenu}
                        >
                          პროფესიული მასწავლებლები
                        </Link>
                      </li>
                    </ul>
                  {/if}
                </li>
                <li class="border-b">
                  <Link
                    to="/partniorebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    პარტნიორები
                  </Link>
                </li>
                <li>
                  <Link
                    to="/misia-khedva-ghirebulebebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    მისია, ხედვა, ღირებულებები
                  </Link>
                </li>
              </ul>
            {/if}
          </li>

          <!-- Programs -->
          <li class="relative">
            <button
              on:click={() => handleMenuClick("programs")}
              class="cursor-pointer py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
            >
              პროგრამები
              <svg
                class="w-4 h-4 ml-2"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19 9l-7 7-7-7"
                />
              </svg>
            </button>

            {#if activeMenu === "programs"}
              <ul
                class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max lg:whitespace-nowrap flex-col items-center"
                transition:fly={{ y: 10, duration: 400 }}
              >
                <li class="border-b">
                  <Link
                    to="/profesiuli-saganmanatleblo-programebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    პროფესიული საგანმანათლებლო პროგრამები
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/profesiuli-momzadebisprofesiuli-gadamzadebis-programebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    პროფესიული მომზადების/პროფესიული გადამზადების პროგრამები
                  </Link>
                </li>
                <li>
                  <Link
                    to="/sasertifikato-programebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    სასერთიფიკატო პროგრამები
                  </Link>
                </li>
              </ul>
            {/if}
          </li>

          <!-- For Students -->
          <li class="relative">
            <button
              on:click={() => handleMenuClick("for-students")}
              class="cursor-pointer py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
            >
              სტუდენტებს
              <svg
                class="w-4 h-4 ml-2"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19 9l-7 7-7-7"
                />
              </svg>
            </button>

            {#if activeMenu === "for-students"}
              <ul
                class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max lg:whitespace-nowrap flex-col items-center"
                transition:fly={{ y: 10, duration: 400 }}
              >
                <li class="border-b">
                  <Link
                    to="/profesiuli-studentis-gzamkvlevi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    პროფესიული სტუდენტის გზამკვლევი
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/msmenelis-gzamkvlevi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    მსმენელის გზამკვლევი
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/studenturi-servisebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    სტუდენტური სერვისები
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/informacia-ssm-da-shshm-pirebistvis"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    ინფორმაცია სსმ და შშმ პირებისთვის
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/sastsavlo-khelshekrulebis-nimushi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    სასწავლო ხელშეკრულების ნიმუში
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/kursdamtavrebulebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    კურსდამთავრებულები
                  </Link>
                </li>

                <!-- Sample of education certificate -->
                <li class="relative border-b">
                  <button
                    on:click={() =>
                      handleSubmenuClick("sample-of-education-certificate")}
                    class="cursor-pointer p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
                  >
                    განათლების დამადასტურებელი დოკუმენტის ნიმუში
                    <svg
                      class="w-4 h-4 ml-2"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M19 9l-7 7-7-7"
                      />
                    </svg>
                  </button>

                  {#if activeSubmenu === "sample-of-education-certificate"}
                    <ul
                      class="lg:absolute text-left lg:left-full lg:top-0 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max lg:whitespace-nowrap flex-col items-center"
                      transition:fly={{ x: -10, duration: 400 }}
                    >
                      <li class="border-b">
                        <Link
                          to="/diplomi"
                          class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                          on:click={closeMenu}
                        >
                          დიპლომი
                        </Link>
                      </li>
                      <li>
                        <Link
                          to="/sertifikati"
                          class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                          on:click={closeMenu}
                        >
                          სერთიფიკატი
                        </Link>
                      </li>
                    </ul>
                  {/if}
                </li>
                <li class="border-b">
                  <Link
                    to="/biblioteka"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    ბიბლიოთეკა
                  </Link>
                </li>
                <li>
                  <Link
                    to="/katalogi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    კატალოგი
                  </Link>
                </li>
              </ul>
            {/if}
          </li>

          <!-- For Applicant -->
          <li class="relative">
            <button
              on:click={() => handleMenuClick("applicants")}
              class="cursor-pointer py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
            >
              აპლიკანთებს
              <svg
                class="w-4 h-4 ml-2"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19 9l-7 7-7-7"
                />
              </svg>
            </button>

            {#if activeMenu === "applicants"}
              <ul
                class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
                transition:fly={{ y: 10, duration: 400 }}
              >
                <li class="border-b">
                  <Link
                    to="/charickhvis-tsesi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    ჩარიცხვის წესი
                  </Link>
                </li>
                <li>
                  <Link
                    to="/gzamkvlevi-aplikantebs"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    გზამკვლევი აპლიკანთებს
                  </Link>
                </li>
              </ul>
            {/if}
          </li>

          <!-- Library -->
          <li class="relative">
            <button
              on:click={() => handleMenuClick("library")}
              class="cursor-pointer py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
            >
              ბიბლიოთეკა
              <svg
                class="w-4 h-4 ml-2"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19 9l-7 7-7-7"
                />
              </svg>
            </button>

            {#if activeMenu === "library"}
              <ul
                class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
                transition:fly={{ y: 10, duration: 400 }}
              >
                <li>
                  <Link
                    to="/bibliotekis-sargeblobis-tsesi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    ბიბლიოთეკის სარგებლობის წესი
                  </Link>
                </li>
                <li class="border-b">
                  <Link
                    to="/eleqtronuli-tsignebi"
                    class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                    on:click={closeMenu}
                  >
                    ელექტრონული წიგნები
                  </Link>
                </li>
              </ul>
            {/if}
          </li>
        </ul>
      </div>
    </div>
  </nav>
</Router>
