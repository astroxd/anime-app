<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  let query = "";

  const tagMap = new Map();
  let tagList = [];
  let nameTagList = [];
  let showMenu;

  function searchAnime() {
    dispatch("searchAnime", {
      query: query,
      tag: tagList,
      nameTagList: nameTagList,
    });
  }

  function createTagMap() {
    tagMap.set(1, "Action");
    tagMap.set(2, "Adventure");
    tagMap.set(3, "Cars");
    tagMap.set(4, "Comedy");
    tagMap.set(5, "Dementia");
    tagMap.set(6, "Demons");
    tagMap.set(7, "Mystery");
    tagMap.set(8, "Drama");
    tagMap.set(9, "Ecchi");
    tagMap.set(10, "Fantasy");
    tagMap.set(11, "Game");
    tagMap.set(12, "Hentai");
    tagMap.set(13, "Historical");
    tagMap.set(14, "Horror");
    tagMap.set(15, "Kids");
    tagMap.set(16, "Magic");
    tagMap.set(17, "Martial Arts");
    tagMap.set(18, "Mecha");
    tagMap.set(19, "Music");
    tagMap.set(20, "Parody");
    tagMap.set(21, "Samurai");
    tagMap.set(22, "Romance");
    tagMap.set(23, "School");
    tagMap.set(24, "Sci Fi");
    tagMap.set(25, "Shoujo");
    tagMap.set(26, "Shoujo Ai");
    tagMap.set(27, "Shounen");
    tagMap.set(28, "Shounen Ai");
    tagMap.set(29, "Space");
    tagMap.set(30, "Sports");
    tagMap.set(31, "Super Power");
    tagMap.set(32, "Vampire");
    tagMap.set(33, "Yaoi");
    tagMap.set(34, "Yuri");
    tagMap.set(35, "Harem");
    tagMap.set(36, "Slice of Life");
    tagMap.set(37, "Supernatural");
    tagMap.set(38, "Military");
    tagMap.set(39, "Police");
    tagMap.set(40, "Psychological");
    tagMap.set(41, "Thriller");
    tagMap.set(42, "Seinen");
    tagMap.set(43, "Josei");
  }
  createTagMap();

  function addTag(key) {
    if (tagList.includes(key)) {
      tagList = tagList.filter((item) => item !== key);
      nameTagList = nameTagList.filter((item) => tagMap.get(key) !== item);
    } else {
      tagList = [...tagList, key];
      nameTagList = [...nameTagList, tagMap.get(key)];
    }
  }

  // Close the dropdown menu if the user clicks outside of it
  window.onclick = function (event) {
    if (
      !event.target.matches(".dropBtn") &&
      !event.target.matches(".dropdown-item")
    ) {
      showMenu = false;
    }
  };
</script>

<div>
  <div class="search">
    <div class="dropdown">
      <button class="dropBtn" on:click={() => (showMenu = !showMenu)}
        >Tag</button
      >
      <div
        class="dropdown-content"
        class:show={showMenu === true}
        id="dropdownID"
      >
        <div class="content-grid">
          {#each [...tagMap] as [key, tag]}
            <li
              class="dropdown-item"
              class:selected={tagList.includes(key)}
              on:click={() => addTag(key)}
            >
              {tag}
            </li>
          {/each}
        </div>
      </div>
    </div>
    <form class="search-box" on:submit={searchAnime}>
      <input
        bind:value={query}
        type="search"
        placeholder="Search for anime..."
      />
    </form>
  </div>

  <!-- <p>
    {nameTagList.join(" > ")}
  </p> -->
</div>

<style>
  div {
    display: flex;
    flex-direction: column;
    word-wrap: break-word;
  }

  .search {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
  }

  button {
    margin: auto 1rem;
    background-color: var(--bg-primary);
    color: white;
    padding: 16px;
    font-size: 16px;
    border: none;
  }

  button:hover {
    background-color: var(--bg-secondary);
  }

  .dropdown {
    position: relative;
    display: inline-block;
  }

  .dropdown-content {
    display: none;
    position: absolute;
    background-color: #f1f1f1;
    min-width: 200px;
    max-width: 300px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
    /* Media Query? */
    max-height: 400px;
    overflow-x: auto;
    overflow-y: scroll;
  }

  .content-grid {
    display: grid;
  }

  .dropdown-content li {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
  }

  .dropdown-content li:hover {
    background-color: rgba(0, 0, 0, 0.2);
  }

  .selected {
    background-color: var(--primary);
  }
  .selected:hover {
    background-color: var(--bg-secondary) !important;
  }

  .show {
    display: block;
  }

  input {
    appearance: none;
    background: none;
    outline: none;
    border: none;

    display: block;
    width: 100%;
    max-width: 400px;
    padding: 16px;
    border-radius: 999px;
    background-color: #eee;

    transition: var(--transition-speed);
  }

  input:focus {
    background-color: #313131;
    color: #fff;
  }

  /* Small Screen */
  @media only screen and (max-width: 600px) {
    /* input{
            margin:auto;
        } */
    /* div{
            justify-content: center;
        } */
    .content-grid {
      grid-template-columns: 1fr;
    }
  }

  /* Large Screen */
  @media only screen and (min-width: 600px) {
    /* input{
            margin-left:auto;
        } */

    /* div{
            justify-content: end;
        } */
    .content-grid {
      grid-template-columns: 1fr 1fr;
    }
  }
</style>
