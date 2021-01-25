<script>
  import AddBook from "./AddBook.svelte";
  import BookList from "./BookList.svelte";
  import SearchBook from "./SearchBook.svelte";

  let books = localStorage.getItem("books")
    ? JSON.parse(localStorage.getItem("books"))
    : [];

  const submitBook = book => {
    const updatedBookList = [...books, book];
    localStorage.setItem("books", JSON.stringify(updatedBookList));
    books = updatedBookList;
  };

  const clearSearch = () => {
    books = localStorage.getItem("books")
      ? JSON.parse(localStorage.getItem("books"))
      : [];
  };

  const search = searchTerm => {
    const searchedBooks = localStorage.getItem("books")
      ? JSON.parse(localStorage.getItem("books"))
      : [];

    books = searchedBooks.filter(({ title }) =>
      title.toLowerCase().includes(searchTerm.toLowerCase())
    );
  };
</script>

<div class="main">
  <h1>Book Finder</h1>

  <SearchBook
    on:search={event => search(event.detail.searchTerm)}
    on:clearSearch={clearSearch}
  />
  <AddBook on:addBook={event => submitBook(event.detail.book)} />
  <BookList {books} />
</div>

<style>
  .main {
    width: 500px;
    max-width: 100%;
    padding: 1em;
    margin: auto;
    text-align: center;
  }
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
</style>
