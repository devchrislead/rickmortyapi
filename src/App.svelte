<script>
  import Character from "./lib/Character.svelte";
  let characters = [];
  let page = 1;
  async function loadCharacters() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
  }
  loadCharacters();
  function nextPage() {
    page++;
    loadCharacters();
  }
  function previousPage() {
    page--;
    loadCharacters();
  }
</script>

;
<h1>Rick and Morty Characters</h1>
<div>
  <button on:click={previousPage} disabled={page === 1}>previousPage</button>
  <button on:click={nextPage}>nextPage</button>
</div>
<div class="container">
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
