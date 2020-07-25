<script>
    export let cells;
</script>

<style>
.lcd-col {
  display: flex;
  align-items: center;
  justify-content: center;
}

.lcd-cell {
  width: 5px;
  height: 5px;
  background-color: #7ec089;
}

.lcd-cell-active {
  background-color: black;
}
</style>

<main>
{#each cells as rows, row}
    <div class="lcd-col">
        {#each rows as cell, col}
            <div 
              class="lcd-cell"
              class:lcd-cell-active="{cell == 1}"
              data-x="{col}"
              data-y="{row}"></div>
        {/each}
    </div>
{/each}
</main>
