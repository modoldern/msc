<script>
  export let teacher;
  import Fa from "svelte-fa";
  import {
    faFacebook,
    faLinkedin,
  } from "@fortawesome/free-brands-svg-icons";
</script>

<div class="w-full overflow-hidden group">
  <div class="relative h-[400px] overflow-hidden">
    <p
      class="absolute flex justify-center items-center w-full gap-5 text-3xl text-mscsecondary-01 bottom-0 z-10 transition-transform duration-300 translate-y-25 group-hover:-translate-y-5"
    >
      {#each teacher.social as social}
        <a href={social.facebook} target="_blank" ><Fa icon={faFacebook} /></a>
        <a href={social.linkedin} target="_blank" ><Fa icon={faLinkedin} /></a>
      {/each}
    </p>
    <img
      src={teacher.image}
      alt={teacher.name}
      class="w-full h-[110%] object-cover transition-transform duration-300 group-hover:-translate-y-5"
    />
  </div>

  <div class="p-4 text-center">
    <h3 class="text-xl font-bold mb-1">{teacher.name}</h3>
    <p class="text-mscprimary text-sm font-semibold mb-2">{teacher.role}</p>
    <p class="text-gray-600 text-sm">{teacher.description}</p>
  </div>
</div>
