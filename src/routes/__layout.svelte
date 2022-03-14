<script>
  import Title from "$lib/Title.svelte";
  import "../styles/global.css";
</script>

<div class="layout">
  <header>
    <Title title="Ruslan's blog" />
  </header>

  <main>
    <slot />
  </main>

  <footer>
    <p>With ❤️ by @ruslangonzalez</p>
  </footer>
</div>

<style>
  .layout {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  main {
    margin: 0 auto;
    padding: 1em;
  }

  footer {
    grid-row-start: 2;
    grid-row-end: 3;
  }

  footer p {
    text-align: center;
    margin: 1em auto;
  }
</style>
