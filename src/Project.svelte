<script>
  export let technologies = [];
  export let code = "";
  export let title = "There was no Title";
  export let description = "There was no Description";
  export let link = "";
  export let image = "";
  let hovered = false;
  import { onMount } from "svelte";
  import { fade, slide } from "svelte/transition";
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";
  import { randomInt } from "d3-random";

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
    flex: 1 1 450px;
    display: flex;
    flex-direction: column;
    border-radius: 15px;
    background-image: linear-gradient(
      353deg,
      hsl(190, 23.1%, 94.9%) 43%,
      hsl(180, 30.8%, 94.9%) 92%
    );
    margin: 1rem;
    padding: 1rem;
    min-width: 300px;
    max-width: 450px;
    height: 450px;
    position: relative;
    cursor: pointer;
    justify-content: space-around;
  }

  .title {
    flex: 0;
    font-family: "Fira Sans";
    font-weight: 400;
    padding-bottom: 2rem;
  }

  .title a {
    color: black;
  }

  .description {
    padding-top: 2rem;
    flex: 1;
    padding: 1rem;
  }

  ul {
    padding-bottom: 3px;
    list-style: none;
    margin-block-start: 0;
    margin-block-end: 0;
    padding-inline-start: 0;
  }
  li {
    display: inline-block;
  }
  li + li {
    padding-left: 1rem;
  }
  img {
    max-height: 200px;
    max-width: 100%;
  }
  .code {
    flex: 1;

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
    transition:slide={{ delay: randomInt(200, 500)() }}
    style="box-shadow: {$shadow * 30}px {$shadow * 15}px #925c77, {$shadow * 45}px
    {$shadow * 21}px #75B9BE, {$shadow * 60}px {$shadow * 30}px #7297A6;"
    class="site">
    <h2
      class="title"
      transition:fade={{ delay: randomInt(250, 500)() }}
      style="text-decoration: {hovered ? 'underline' : 'none'};">
      <a href={link}>{title}</a>
    </h2>
    <img src={image} alt="A screenshot of {title}" />
    <div
      class="description"
      transition:fade={{ delay: randomInt(250, 1000)() }}>
      {description}
    </div>
    <div class="code">
      <ul>
        {#each technologies as technology}
          <li in:typewriter={{ speed: randomInt(150, 300)() }}>{technology}</li>
        {/each}
      </ul>
      {#if code != ''}<a href={code}>Source Code</a>{/if}
    </div>
  </div>
{/if}
