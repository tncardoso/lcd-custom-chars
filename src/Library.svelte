<script>
  import Preview from './Preview.svelte';

    let library = [
        {
            name: 'Heart',
            data: [
                [0,0,0,0,0],
                [0,0,0,0,0],
                [0,1,0,1,0],
                [1,1,1,1,1],
                [1,1,1,1,1],
                [0,1,1,1,0],
                [0,0,1,0,0],
                [0,0,0,0,0]
            ]
        }
    ];
</script>

<style>
</style>

<main>
 <section class="section">
    <div class="container">
        <h1 class="title">Library</h1>
        <!--<h2 class="subtitle">oi</h2>-->

        <div class="columns is-multiline">
        {#each library as char, i}
        {#each { length: 8 } as _, row}

        <div class="column is-2 has-text-centered">
            <Preview cells={char.data} />
            {char.name}
        </div>
        {/each}
        {/each}
        </div>
    </div>
  </section>
</main>