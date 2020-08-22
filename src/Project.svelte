<script>
  export let technologies = [];
  export let code = "";
  export let title = "There was no Title";
  export let description = "There was no Description";
  export let link;
  export let image = "";
  let hovered = false;
  import { onMount } from "svelte";
  import { fade, slide } from "svelte/transition";
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";

  const shadow = tweened(0, { duration: 500, easing: cubicOut });

  function handleClick() {
    window.location = link;
  }

  function handleMouseEnter() {
    shadow.set(1);
    hovered = true;
  }

  function handleMouseLeave() {
    shadow.set(0);
    hovered = false;
  }

  function typewriter(node, { speed = 50 }) {
    const valid =
      node.childNodes.length === 1 &&
      node.childNodes[0].nodeType === Node.TEXT_NODE;

    if (!valid) {
      throw new Error(
        `This transition only works on elements with a single text node child`
      );
    }

    const text = node.textContent;
    const duration = text.length * speed;

    return {
      duration,
      tick: (t) => {
        const i = ~~(text.length * t);
        node.textContent = text.slice(0, i);
      },
    };
  }

  let mounted = false;
  onMount(() => (mounted = true));
</script>

<style>
  .site {
    border-radius: 15px;
    border: solid;
    border-width: thin;
    margin: 1rem;
    padding: 1rem;
    min-width: 300px;
    max-width: 450px;
    min-height: 500px;
    position: relative;
    cursor: pointer;
  }

  .title {
    font-family: "Fira Sans";
    font-weight: 400;
  }

  .title a {
    color: black;
  }

  .description {
    padding: 1rem;
  }

  ul {
    padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  li + li {
    padding-left: 1rem;
  }
  img {
    width: 100%;
    height: auto;
  }
  .code {
    font-family: "Fira Code";
  }
</style>

{#if mounted}
  <div
    on:click={handleClick}
    on:mouseenter={handleMouseEnter}
    on:touchstart={handleMouseEnter}
    on:mouseleave={handleMouseLeave}
    on:touchend={handleMouseLeave}
    transition:slide={{ delay: 200 }}
    style="box-shadow: {$shadow * 30}px {$shadow * 15}px #925c77, {$shadow * 45}px
    {$shadow * 21}px #75B9BE, {$shadow * 60}px {$shadow * 30}px #7297A6;"
    class="site">
    <h2
      class="title"
      transition:fade={{ delay: 250 }}
      style="text-decoration: {hovered ? 'underline' : 'none'};">
      <a href={link}>{title}</a>
    </h2>
    <img src={image} alt="A screenshot of {title}" />
    <div class="description" transition:fade={{ delay: 500 }}>
      {description}
    </div>
    <ul class="code">
      {#each technologies as technology}
        <li in:typewriter={{ speed: 175 }}>{technology}</li>
      {/each}
    </ul>
    <a class="code" href={code}>Source Code</a>
  </div>
{/if}
