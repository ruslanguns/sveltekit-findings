<script context="module">
  export async function load({ fetch }) {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    const posts = await res.json();

    if (!res.ok) {
      return {
        status: res.status,
        message: posts.message,
        error: new Error(posts.message || "Something went wrong"),
      };
    }

    return {
      props: {
        posts,
      },
    };
  }
</script>

<script>
  export let posts = [];
</script>

<div class="posts">
  {#each posts.splice(0, 10) as post}
    <a href={"/article/" + post.id}>
      <div class="post">
        <h4 title={post.title}>{post.title}</h4>
        <p>{post.body}</p>
      </div>
    </a>
  {/each}
</div>

<style>
  .posts {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1em;
  }

  a {
    text-decoration: none;
  }

  .post {
    padding: 1em;
    background: rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    transition: background 0.2s ease;
  }

  .post:hover {
    background: rgba(0, 0, 0, 0.3);
    cursor: pointer;
  }

  .post h4 {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 15ch;
  }
</style>
