<script lang="ts">
  import { darkmode } from "$lib/stores/darkmode";
  import SunIcon from '$lib/components/svg/SunIcon.svelte';
  import MoonIcon from '$lib/components/svg/MoonIcon.svelte';
  import { slide }from "svelte/transition";

  let inTransition = {
    duration: 400, delay: 500
  };

  let outTransition = {
    duration: 400
  }

  function toggleDarkmode() {
    if ($darkmode) {
      $darkmode = false;
      document.documentElement.classList.remove("dark");
      localStorage.setItem("theme", "light");
    } else {
      $darkmode = true;
      document.documentElement.classList.add("dark");
      localStorage.setItem("theme", "dark");
    }
  }
  
</script>

<button 
  class="p-2 text-purple-8000 dark:text-yellow-200"
  on:click={toggleDarkmode}
>
  {#if $darkmode}
    <div
      in:slide={inTransition}
      out:slide={outTransition}
    >
    <SunIcon class="w-8 h-8 fill-current" />
    </div>
  {:else}
    <div>
      <MoonIcon class="w-8 h-8 fill-current" />
    </div>
  {/if}
</button>

