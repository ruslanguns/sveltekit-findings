<script context="module">

  async function load({ fetch }) {
    const res = await fetch('https://api.thecatapi.com/v1/images/search');
    const cat = await res.json();
    
    return {
      props: {
        src: cat[0].url
      }
    }
  }

</script>

<script>
  import "../styles/cat.css";

  export let cat;
  let loading = false;
  
  const loadRandomCat = () => {

  }
  
  
  // import { onMount } from "svelte";
  // onMount(async () => {
  //   await loadRandomCat();
  // });

  // const loadRandomCat = async () => {
  //   loading = true;
  //   await new Promise((resolve) => setTimeout(resolve, 500));

  //   const res = await fetch("https://api.thecatapi.com/v1/images/search");
  //   const json = await res.json();
  //   cat = json[0];
  //   loading = false;
  // };
</script>

<div class="wrapper">
  <button disabled={loading} on:click={loadRandomCat}>
    Load a random cat!
  </button>
  {#if loading}
    loading...
  {/if}

  {#if cat}
    <img src={cat.url} alt="Random Cat" />
  {/if}
</div>
