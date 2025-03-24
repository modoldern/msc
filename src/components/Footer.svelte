<script>
  import { onMount } from "svelte";

  // Props to receive data
  export let footerData;
</script>

<footer
  class="bg-mscsecondary-01 w-full flex flex-col items-center justify-center gap-40 text-msclight py-12 min-h-[715px]"
>
  <div class="w-full px-5 xl:px-0 xl:w-6xl grid sm:grid-cols-2 xl:grid-cols-3 gap-8 h-auto">
    <!-- Questions Section -->
    <div class="flex flex-col items-start text-left">
      <h2 class="text-xl font-bold mb-6">გაქვთ შეკითხვები?</h2>
      <div class="space-y-4 flex flex-col">
        <p class="flex items-start">
          <span class="mr-2"
            ><svg
              xmlns="http://www.w3.org/2000/svg"
              height="24px"
              viewBox="0 -960 960 960"
              width="24px"
              fill="#e8eaed"
              ><path
                d="M480-480q33 0 56.5-23.5T560-560q0-33-23.5-56.5T480-640q-33 0-56.5 23.5T400-560q0 33 23.5 56.5T480-480Zm0 294q122-112 181-203.5T720-552q0-109-69.5-178.5T480-800q-101 0-170.5 69.5T240-552q0 71 59 162.5T480-186Zm0 106Q319-217 239.5-334.5T160-552q0-150 96.5-239T480-880q127 0 223.5 89T800-552q0 100-79.5 217.5T480-80Zm0-480Z"
              /></svg
            ></span
          >
          {footerData.address}, {footerData.city}, {footerData.state}, {footerData.country}
        </p>
        <p class="flex items-start">
          <span class="mr-2"
            ><svg
              xmlns="http://www.w3.org/2000/svg"
              height="24px"
              viewBox="0 -960 960 960"
              width="24px"
              fill="#e8eaed"
              ><path
                d="M798-120q-125 0-247-54.5T329-329Q229-429 174.5-551T120-798q0-18 12-30t30-12h162q14 0 25 9.5t13 22.5l26 140q2 16-1 27t-11 19l-97 98q20 37 47.5 71.5T387-386q31 31 65 57.5t72 48.5l94-94q9-9 23.5-13.5T670-390l138 28q14 4 23 14.5t9 23.5v162q0 18-12 30t-30 12ZM241-600l66-66-17-94h-89q5 41 14 81t26 79Zm358 358q39 17 79.5 27t81.5 13v-88l-94-19-67 67ZM241-600Zm358 358Z"
              /></svg
            ></span
          >
          {footerData.phone}
        </p>
        <p class="flex items-start">
          <span class="mr-2"
            ><svg
              xmlns="http://www.w3.org/2000/svg"
              height="24px"
              viewBox="0 -960 960 960"
              width="24px"
              fill="#e8eaed"
              ><path
                d="M160-160q-33 0-56.5-23.5T80-240v-480q0-33 23.5-56.5T160-800h640q33 0 56.5 23.5T880-720v480q0 33-23.5 56.5T800-160H160Zm320-280L160-640v400h640v-400L480-440Zm0-80 320-200H160l320 200ZM160-640v-80 480-400Z"
              /></svg
            ></span
          >
          {footerData.email}
        </p>
      </div>
    </div>
    <!-- Links -->
    <div class="flex flex-col items-start text-left">
      <h2 class="text-xl font-bold mb-6">ბმულები</h2>
      <ul class="space-y-2">
        {#each footerData.links as link}
          <li>
            <a
              href="#{link.toLowerCase()}"
              class="hover:text-mscsecondary-02 transition-colors"
            >
              → {link}
            </a>
          </li>
        {/each}
      </ul>
    </div>

    <!-- Map Section -->
    <div class="relative flex flex-col items-start text-left">
      <h2 class="text-xl font-bold mb-6">ადგილმდებარეობა</h2>
      <div class="w-full h-[180px] overflow-hidden">
        <iframe
          title="Location Map"
          width="100%"
          height="200px"
          frameborder="0"
          scrolling="no"
          marginheight="0"
          marginwidth="0"
          src="https://www.openstreetmap.org/export/embed.html?bbox=44.798%2C41.482%2C44.806%2C41.486&layer=mapnik&marker=41.484127%2C44.801767&zoom=16"
        ></iframe>
      </div>

      <!-- Connect With Us -->
      <div class="mt-6">
        <h2 class="text-xl font-bold mb-4">შემოგვიერთდით</h2>
        <div class="flex space-x-4">
          <a
            href={footerData.socialLinks.twitter}
            class="hover:text-mscsecondary-01"
            aria-label="Follow us on Twitter"
          >
            <span class="sr-only">Twitter</span>
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"
              />
            </svg>
          </a>
          <a
            href={footerData.socialLinks.facebook}
            class="hover:text-mscsecondary-02"
            aria-label="Follow us on Facebook"
            target="_blank"
          >
            <span class="sr-only">Facebook</span>
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"
              />
            </svg>
          </a>
          <a
            href={footerData.socialLinks.instagram}
            class="hover:text-purple-400"
            aria-label="Follow us on Instagram"
          >
            <span class="sr-only">Instagram</span>
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M12 0C8.74 0 8.333.015 7.053.072 5.775.132 4.905.333 4.14.63c-.789.306-1.459.717-2.126 1.384S.935 3.35.63 4.14C.333 4.905.131 5.775.072 7.053.012 8.333 0 8.74 0 12s.015 3.667.072 4.947c.06 1.277.261 2.148.558 2.913.306.788.717 1.459 1.384 2.126.667.666 1.336 1.079 2.126 1.384.766.296 1.636.499 2.913.558C8.333 23.988 8.74 24 12 24s3.667-.015 4.947-.072c1.277-.06 2.148-.262 2.913-.558.788-.306 1.459-.718 2.126-1.384.666-.667 1.079-1.335 1.384-2.126.296-.765.499-1.636.558-2.913.06-1.28.072-1.687.072-4.947s-.015-3.667-.072-4.947c-.06-1.277-.262-2.149-.558-2.913-.306-.789-.718-1.459-1.384-2.126C21.319 1.347 20.651.935 19.86.63c-.765-.297-1.636-.499-2.913-.558C15.667.012 15.26 0 12 0zm0 2.16c3.203 0 3.585.016 4.85.071 1.17.055 1.805.249 2.227.415.562.217.96.477 1.382.896.419.42.679.819.896 1.381.164.422.36 1.057.413 2.227.057 1.266.07 1.646.07 4.85s-.015 3.585-.074 4.85c-.061 1.17-.256 1.805-.421 2.227-.224.562-.479.96-.899 1.382-.419.419-.824.679-1.38.896-.42.164-1.065.36-2.235.413-1.274.057-1.649.07-4.859.07-3.211 0-3.586-.015-4.859-.074-1.171-.061-1.816-.256-2.236-.421-.569-.224-.96-.479-1.379-.899-.421-.419-.69-.824-.9-1.38-.165-.42-.359-1.065-.42-2.235-.045-1.26-.061-1.649-.061-4.844 0-3.196.016-3.586.061-4.861.061-1.17.255-1.814.42-2.234.21-.57.479-.96.9-1.381.419-.419.81-.689 1.379-.898.42-.166 1.051-.361 2.221-.421 1.275-.045 1.65-.06 4.859-.06l.045.03zm0 3.678c-3.405 0-6.162 2.76-6.162 6.162 0 3.405 2.76 6.162 6.162 6.162 3.405 0 6.162-2.76 6.162-6.162 0-3.405-2.76-6.162-6.162-6.162zM12 16c-2.21 0-4-1.79-4-4s1.79-4 4-4 4 1.79 4 4-1.79 4-4 4zm7.846-10.405c0 .795-.646 1.44-1.44 1.44-.795 0-1.44-.646-1.44-1.44 0-.794.646-1.439 1.44-1.439.793-.001 1.44.645 1.44 1.439z"
              />
            </svg>
          </a>
        </div>
      </div>
    </div>
  </div>

  <!-- Copyright -->
  <div class="text-center text-sm w-full h-auto break-all px-5 xl:px-0">
    Copyright ©2024 - {new Date().getFullYear()} MSC, Inc. All rights reserved |
    This page is made with by
    <a
      href="https://github.com/modoldern"
      class="hover:bg-mscsecondary-02 px-1 py-1 ml-1 border-y border-dotted"
      target="_blank">Modoldern</a
    >
  </div>
</footer>
