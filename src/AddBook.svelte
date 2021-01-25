<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let title = "",
    author = "";
  let rating = 1;
  const onTitleChange = e => {
    title = e.target.value;
  };
  const onAuthorChange = e => {
    author = e.target.value;
  };
  const onRatingSelect = e => {
    rating = e.target.value;
  };
  const addBook = () => {
    if (title && author) {
      dispatch("addBook", {
        book: {
          title,
          author,
          rating
        }
      });
      title = "";
      author = "";
      rating = 1;
    }
  };
</script>

<div class="main">
  <input
    placeholder="Title"
    type="text"
    value={title}
    on:keyup={onTitleChange}
  />
  <input
    placeholder="Author"
    type="text"
    value={author}
    on:keyup={onAuthorChange}
  />

  <!-- svelte-ignore a11y-no-onchange -->
  <select value={rating} on:change={onRatingSelect}>
    <option value={1}>1</option>
    <option value={2}>2</option>
    <option value={3}>3</option>
    <option value={4}>4</option>
    <option value={5}>5</option>
  </select>

  <button on:click={addBook} disabled={!title || !author}>Add</button>
</div>

<style>
  .main {
    display: flex;
  }
  .main input {
    flex: 1;
    margin-right: 10px;
  }
  .main select {
    width: 150px;
    margin-right: 10px;
  }
</style>
