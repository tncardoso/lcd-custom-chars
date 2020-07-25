<script>
  import { createEventDispatcher } from 'svelte';
  import { onMount } from 'svelte';
  import Preview from './Preview.svelte';

    const dispatch = createEventDispatcher();
    let library = [];

    onMount(async () => {
        const res = await fetch('library.json');
        library = await res.json();
    });

    function load(name, cells) {
      dispatch('message', {
        name: name,
        cells: cells
      });
    }
</script>

<style>
.pointer {cursor: pointer;}
</style>

<main>
 <section class="section">
    <div class="container">
        <h1 class="title">Library</h1>
        <h2 class="subtitle">Click to load on editor</h2>

        <div class="columns is-multiline">
        {#each library as char, i}
        <div
          class="column is-2 has-text-centered pointer"
          on:click={() => load(char.name, char.data) }>
            <Preview
              cells={char.data}/>
            {char.name}
        </div>
        {/each}
        </div>
    </div>
  </section>
</main>