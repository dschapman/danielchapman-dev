<script>
  import Project from "./Project.svelte";
  import Bio from "./Bio.svelte";
  import { slide } from "svelte/transition";
  import { onMount } from "svelte";
</script>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Fira+Code:wght@300&family=Fira+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Roboto:ital,wght@0,300;0,500;1,300;1,500&display=swap");

  * {
    text-align: center;

    margin: 0 auto;
    font-family: "Roboto";
    font-weight: 300;
  }

  header {
    padding-bottom: 2rem;
  }
  main {
    display: grid;
    grid-gap: 1rem;
    grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
    justify-content: center;
    place-items: center;
  }

  footer {
    margin-top: 1rem;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-family: "Fira Sans", "Arial", sans-serif;
  }

  h1 {
    font-size: 4em;
    color: #925c77;
    font-weight: 700;
  }
  h3 {
    font-size: 1.5em;
  }
</style>

<header>
  <h1>Daniel Chapman</h1>
  <h3>A list of sites that I've built</h3>
</header>
<main>
  <Project
    technologies={['Gatsby', 'React', 'Markdown']}
    title={'dschapman.com'}
    image={'dschapman-com.png'}
    description="A digital garden, constructed to hold articles, poems, and
    notes. Featuring bidirectional links, link previews, and self-generating
    OpenGraph images."
    link={'https://dschapman.com'} />

  <Project
    technologies={['Svelte', 'HTML', 'CSS']}
    title={'DanielChapman.dev'}
    image={'danielchapman-dev.png'}
    description={"This is the site that you're looking at now. A Svelte site with some simple styling and a couple snazzy animations."}
    ink={'https://danielchapman.dev'} />
</main>
<footer>
  Contact me:
  <a href="mailto:daniel@dschapman.com">daniel@dschapman.com</a>
</footer>
