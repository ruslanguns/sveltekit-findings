<script>
  export let title = "This is my first Sveltekit App";
</script>

<h3><a href="/">{title}</a></h3>
<a href="/cats">🐱 Show me a cat!</a>

<style>
  h3 {
    margin: 0;
    padding: 0;
    text-align: center;
  }

  a {
    text-align: center;
    padding-top: 0.4em;
    display: block;
    text-decoration: none;
  }
</style>
