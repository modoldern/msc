<script>
  import { fade, slide, fly, scale } from "svelte/transition";
  let visible = false;

  // Sayfa yüklendiğinde animasyonu tetikle
  import { onMount } from "svelte";
  onMount(() => {
    visible = true;
  });

  // Single state to track which menu/submenu is currently open
  let activeMenu = null;
  let activeSubmenu = null;
  let isOpen = false;

  // Function to handle main menu clicks
  const handleMenuClick = (menuId) => {
    if (activeMenu === menuId) {
      activeMenu = null;
      activeSubmenu = null;
    } else {
      activeMenu = menuId;
      activeSubmenu = null;
    }
  };

  // Function to handle submenu clicks
  const handleSubmenuClick = (submenuId) => {
    if (activeSubmenu === submenuId) {
      activeSubmenu = null;
    } else {
      activeSubmenu = submenuId;
    }
  };
</script>

<nav class="text-msclight h-full w-full lg:flex">
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
      <ul transition:fly={{ y: 10, duration: 300 }}
        class="flex flex-col items-start lg:flex-row lg:mt-0 text-sm font-medium"
      >
        <!-- Home -->
        <li>
          <a href="/" class="block py-2 px-2 hover:text-mscsecondary-02"
            >მთავარი</a
          >
        </li>

        <!-- About Us -->
        <li class="relative">
          <button
            on:click={() => handleMenuClick("about")}
            class="py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
              class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
              transition:fly={{ y: 10, duration: 400 }}
            >
              <li class="border-b">
                <a
                  href="/structure"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  სტრუქტურა
                </a>
              </li>

              <!-- Teachers submenu -->
              <li class="relative border-b">
                <button
                  on:click={() =>
                    handleSubmenuClick("vocational-education-teachers")}
                  class="p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
                      <a
                        href="/vocational-education-teacher-program-implementer-recruitment-procedure"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        პროფესიული განათლების მასწავლებლის/პროგრამის
                        განმახორციელებლის სამსახურში მიღების წესი
                      </a>
                    </li>
                    <li class="border-b">
                      <a
                        href="/vocational-teacher-recruitment-rules"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        პროფესიული მასწავლებლის სამსახურში მიღების წესები
                      </a>
                    </li>
                    <li>
                      <a
                        href="/vocational-teachers-guides"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        პროფესიული მასწავლებლის გზამკვლევები
                      </a>
                    </li>
                  </ul>
                {/if}
              </li>
              <!-- Other menu items -->
              <li class="border-b">
                <a
                  href="/action-plans"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  სამოქმედო გეგმები
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/regulatory-acts"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  მარეგულირებელი აქტები
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/authorization-decision"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  ავტორიზაციის გადაწყვეტილება
                </a>
              </li>
              <!-- Personnel -->
              <li class="relative border-b">
                <button
                  on:click={() => handleSubmenuClick("personnel")}
                  class="p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
                      <a
                        href="/administration"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        ადმინისტრაცია
                      </a>
                    </li>
                    <li>
                      <a
                        href="/vocational-teachers"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        პროფესიული მასწავლებლები
                      </a>
                    </li>
                  </ul>
                {/if}
              </li>
              <li class="border-b">
                <a
                  href="/partners"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  პარტნიორები
                </a>
              </li>
              <li>
                <a
                  href="/mission-vision-values"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  მისია, ხედვა, ღირებულებები
                </a>
              </li>
            </ul>
          {/if}
        </li>

        <!-- Programs -->
        <li class="relative">
          <button
            on:click={() => handleMenuClick("programs")}
            class="py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
              class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
              transition:fly={{ y: 10, duration: 400 }}
            >
              <li class="border-b">
                <a
                  href="/vocational-educational-programs"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  პროფესიული საგანმანათლებლო პროგრამები
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/vocational-training-retraining-programs"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  პროფესიული მომზადების/პროფესიული გადამზადების პროგრამები
                </a>
              </li>
              <li>
                <a
                  href="/certificate-programs"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  სასერთიფიკატო პროგრამები
                </a>
              </li>
            </ul>
          {/if}
        </li>

        <!-- For Students -->
        <li class="relative">
          <button
            on:click={() => handleMenuClick("for-students")}
            class="py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
              class="lg:absolute text-left lg:left-0 lg:mt-4 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
              transition:fly={{ y: 10, duration: 400 }}
            >
              <li class="border-b">
                <a
                  href="/vocational-student-guide"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  პროფესიული სტუდენტების გზამკვლევი
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/listeners-guide"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  მსმენელის გზამკვნელი
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/student-services"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  სტუდენტური სერვისები
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/information-for-disabled-people"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  ინფორმაცია სსმ და შშმ პირებისთვის
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/sample-training-contract"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  სასწავლო ხელშეკრულების ნიმუში
                </a>
              </li>
              <li class="border-b">
                <a
                  href="/graduates"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  კურსდამთავრებულები
                </a>
              </li>

              <!-- Sample of education certificate -->
              <li class="relative border-b">
                <button
                  on:click={() =>
                    handleSubmenuClick("sample-of-education-certificate")}
                  class="p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
                    class="lg:absolute text-left lg:left-full lg:top-0 bg-mscsecondary-02 lg:bg-mscsecondary-01 w-full lg:w-max whitespace-nowrap flex-col items-center"
                    transition:fly={{ x: -10, duration: 400 }}
                  >
                    <li class="border-b">
                      <a
                        href="/diploma"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        დიპლომი
                      </a>
                    </li>
                    <li>
                      <a
                        href="/certificate"
                        class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                      >
                        სერთიფიკატი
                      </a>
                    </li>
                  </ul>
                {/if}
              </li>
              <li class="border-b">
                <a
                  href="/library"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  ბიბლიოთეკა
                </a>
              </li>
              <li>
                <a
                  href="/catalog"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  კატალოგი
                </a>
              </li>
            </ul>
          {/if}
        </li>

        <!-- For Applicant -->
        <li class="relative">
          <button
            on:click={() => handleMenuClick("applicants")}
            class="py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
                <a
                  href="/enrollment-rules"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  ჩარიცხვის წესი
                </a>
              </li>
              <li>
                <a
                  href="/guide-for-applicants"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  გზამკვლევი აპლიკანთებს
                </a>
              </li>
            </ul>
          {/if}
        </li>

        <!-- Library -->
        <li class="relative">
          <button
            on:click={() => handleMenuClick("library")}
            class="py-2 px-2 hover:text-mscsecondary-02 flex justify-center items-center w-full lg:w-auto"
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
              <li class="border-b">
                <a
                  href="/e-books"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  ელექტრონული წიგნები
                </a>
              </li>
              <li>
                <a
                  href="/library-usage-rules"
                  class="block p-2 hover:text-mscaccent lg:hover:text-mscsecondary-02"
                >
                  ბიბლიოთეკის სარგებლობის წესი
                </a>
              </li>
            </ul>
          {/if}
        </li>
      </ul>
    </div>
  </div>
</nav>
