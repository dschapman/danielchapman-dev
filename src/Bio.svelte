<script>
  import { slide } from "svelte/transition";
  let visible = false;
  let symbol = "▽";
</script>

<style>
  h1 {
    font-family: "Fira Sans", "Arial", sans-serif;
    font-size: 4em;
    color: #925c77;
    font-weight: 700;
    display: inline;
    cursor: pointer;
  }

  .bio {
    padding-bottom: 2rem;
  }
  .name {
    display: inline-block;
  }
  .symbol {
    padding-left: 1rem;
    font-size: 2em;
    display: inline;
    font-family: "Fira Code";
    cursor: pointer;
  }
  .intro {
    max-width: 600px;
  }
</style>

<div class="bio">
  <span class="name" on:click={() => (visible = !visible)}>
    <h1>Daniel Chapman</h1>
    <span class="symbol">{visible ? 'x' : '▽'}</span>
  </span>
  {#if visible}
    <div class="intro" transition:slide>
      Hi, I live and work in Virginia and write code until it becomes
      functioning websites. I've worked in React, Gatsby, and Svelte to build
      the sites listed below, but I'm always interested in learning new
      technologies!
    </div>
  {/if}

</div>
