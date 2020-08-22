<script>
  export let technologies = [];
  export let title = "There was no Title";
  export let description = "There was no Description";
  export let link;
  export let image = "";
  import { onMount } from "svelte";
  import { fade, slide } from "svelte/transition";
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";

  const shadowx = tweened(0, { duration: 500, easing: cubicOut });
  const shadowy = tweened(0, { duration: 500, easing: cubicOut });

  function handleClick() {
    window.location = link;
  }

  let mounted = false;
  onMount(() => (mounted = true));
</script>

<style>
  .site {
    border-radius: 15px;
    border-width: 0px;
    border: solid;
    margin: 1rem;
    padding: 1rem;
    width: 450px;
    min-height: 500px;
    position: relative;
    cursor: pointer;
  }

  .title {
    font-family: "Fira Sans";
  }
  .title a {
    color: black;
    text-decoration: none;
  }

  .description {
    padding: 1rem;
  }

  ul {
    padding: 0;
    list-style: none;
  }
  li {
    font-family: "Fira Code";
    display: inline-block;
  }
  li + li {
    padding-left: 1rem;
  }
  img {
    width: 100%;
    height: auto;
  }
</style>

{#if mounted}
  <div
    on:click={handleClick}
    on:mouseenter={() => {
      shadowx.set(40);
      shadowy.set(20);
    }}
    on:mouseleave={() => {
      shadowx.set(0);
      shadowy.set(0);
    }}
    transition:slide={{ delay: 200 }}
    style="box-shadow: {$shadowx}px {$shadowy}px #925c77"
    class="site">
    <h2 class="title" transition:fade={{ delay: 250 }}>
      <a href={link}>{title}</a>
    </h2>
    <img src={image} alt="A screenshot of my website" />
    <div class="description" transition:fade={{ delay: 500 }}>
      {description}
    </div>
    <ul transition:fade={{ delay: 1000 }}>
      {#each technologies as technology}
        <li>{technology}</li>
      {/each}
    </ul>
  </div>
{/if}
