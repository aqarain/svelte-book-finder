<script>
  export let books;
</script>

{#each books as book (book.title)}
  <div>
    <h3>{book.title}</h3>
    <h4>{book.author}</h4>
    <p>Rating: {book.rating} star</p>
  </div>
{/each}

<style>
  div {
    text-align: left;
    padding-bottom: 10px;
    border-bottom: 1px solid gray;
  }
  h4 {
    color: gray;
  }
</style>
