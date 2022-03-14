<script context="module">
  export async function load({ fetch, params }) {
    const id = params.id;
    const res = await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`);
    const post = await res.json();

    if (!res.ok) {
      return {
        status: 301,
        redirect: "/",
      };
    }

    const resUser = await fetch(
      `https://jsonplaceholder.typicode.com/users/${post.userId}`
    );
    const user = await resUser.json();

    const resComments = await fetch(
      `https://jsonplaceholder.typicode.com/comments?postId=${post.id}`
    );
    const comments = await resComments.json();

    return {
      props: {
        post,
        user,
        comments,
      },
    };
  }
</script>

<script>
  import { goto } from "$app/navigation";
  export let post;
  export let user;
  export let comments = [];

  const handleGoPrevius = () => {
    goto(`/`);
  };
</script>

<section>
  <div class="previous-btn" on:click={handleGoPrevius}>
    &lArr; Go previous page
  </div>
  <article>
    <h1>{post.title}</h1>
    <p>Author: {user.username}</p>

    <picture>
      <source
        media="(min-width: 640px)"
        srcset="https://source.unsplash.com/random/640×450	"
      />
      <source
        media="(min-width: 850px)"
        srcset="https://source.unsplash.com/random/850×640"
      />

      <img src="https://source.unsplash.com/random/1280×960" alt={post.title} />
    </picture>
    <p>{post.body}</p>
  </article>
  <aside>
    <h5>Comments...</h5>
    <ul class="comments">
      {#each comments as comment}
        <li>
          <p>{comment.body}</p>
          <small>— by {comment.email}</small>
        </li>
      {/each}

      {#if comments.length === 0}
        <li>No comments</li>
      {/if}
    </ul>
  </aside>
</section>

<style>
  .previous-btn {
    background-color: rgba(0, 0, 0, 0.1);
    display: inline-block;
    padding: 0.5em;
  }

  .previous-btn:hover {
    cursor: pointer;
    background-color: rgba(0, 0, 0, 0.3);
  }

  section {
    max-width: 600px;
  }

  img {
    width: 100%;
  }

  .comments {
    list-style: none;
    padding: 0;
  }

  .comments li {
    margin-bottom: 0.5rem;
    background: rgba(0, 0, 0, 0.1);
    padding: 1em;
    border-radius: 0.3em;
  }
</style>
