<script>
  import { slide } from "svelte/transition";
  let visible = false;
  let symbol = "▽";
  export let intro;
</script>

<style>
  h1 {
    font-family: "Fira Sans", "Arial", sans-serif;
    font-size: 4em;
    color: #925c77;
    font-weight: 700;
    display: inline;
  }
  .about h2 {
    padding-right: 3rem;
    align-self: center;
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
  .about {
    max-width: 600px;
    display: flex;
    justify-content: space-between;
    margin-top: 2rem;
    background-color: white;
  }
  .about .intro {
    flex: 1;
    text-align: left;
  }
</style>

<div class="bio">
  <span class="name" on:click={() => (visible = !visible)}>
    <h1>Daniel Chapman</h1>

    <span class="symbol">{visible ? 'x' : '▽'}</span>
  </span>
  {#if visible}
    <div class="about" transition:slide>
      <h2>About Me</h2>
      <div class="intro">{intro}</div>
    </div>
  {/if}

</div>
