<script>
  import Project from "./Project.svelte";
  import Bio from "./Bio.svelte";
</script>

<style>
  main {
    justify-content: center;
    place-items: center;
  }
  .projects {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  footer {
    margin-top: 3rem;
  }

  h3 {
    font-family: "Fira Sans", "Arial", sans-serif;

    font-size: 1.5em;
  }

  footer ul {
    margin: 0 auto;
    padding: 0;
    padding-top: 1rem;
    list-style: none;
    margin-block-start: 0;
    margin-block-end: 0;
    padding-inline-start: 0;
  }
  footer li {
    display: inline-block;
    padding-bottom: 6px;
  }
  footer li + li {
    display: inline-block;
    padding-left: 1rem;
  }
</style>

<main>
  <Bio />
  <h3>A list of sites that I've built</h3>
  <div class="projects">
    <Project
      technologies={['Gatsby', 'React', 'Markdown']}
      title={'dschapman.com'}
      image={'dschapman-com.png'}
      description="A digital garden, constructed to hold articles, poems, and
      notes. Featuring bidirectional links, link previews, and self-generating
      OpenGraph images."
      link={'https://dschapman.com'}
      code={'https://github.com/dschapman/dschapman-com'} />

    <Project
      technologies={['Svelte', 'HTML', 'CSS']}
      title={'danielchapman.dev'}
      image={'danielchapman-dev.png'}
      description={"This is the site that you're looking at now. A Svelte site with some simple styling and a couple snazzy animations."}
      link={'https://danielchapman.dev/'}
      code={'https://github.com/dschapman/danielchapman-dev'} />
  </div>
</main>
<footer>
  <h3>Contact me</h3>
  <ul>
    <li>
      <a href="mailto:daniel@dschapman.com">Email</a>
    </li>
    <li>
      <a href="twitter.com/ds_chapman">Twitter</a>

    </li>
    <li>
      <a href="https://www.linkedin.com/in/daniel-chapman-63695271/">
        LinkedIn
      </a>
    </li>
  </ul>
</footer>
