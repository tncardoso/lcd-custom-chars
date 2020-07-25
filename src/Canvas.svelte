<script>
  import Preview from './Preview.svelte';
  import Library from './Library.svelte';

  const ROWS = 8;
  const COLS = 5;
  var cells = [];
  var code = "";
  clear();

  function buildCode() {
    code = "byte customChar[] = {\n";
    for (var row = 0; row < ROWS; row++) {
      code += "    B";
      for (var col = 0; col < COLS; col++) {
        if (cells[row][col]) {
          code += "1";
        } else {
          code += "0";
        }
      }
      if (row < ROWS-1) { code += ","; }
      code += "\n";
    }
    code += "};"
  }

  function buildCodeJson() {
    code = "";
    for (var row = 0; row < ROWS; row++) {
      code += "    [";
      for (var col = 0; col < COLS; col++) {
        if (cells[row][col]) {
          code += "1";
        } else {
          code += "0";
        }
        if (col != COLS-1) { code += ","; }
      }
      code += "]";
      if (row < ROWS-1) { code += ","; }
      code += "\n";
    }
  }
  
  function cellClicked(row, col) {
    cells[row][col] = !cells[row][col];
    buildCode();
  }

  function clear() {
      cells = new Array(ROWS);
      for (var row = 0; row < ROWS; row++) {
        cells[row] = new Array(COLS);
      }
      buildCode();
  }

  function load(event) {
    cells = event.detail.cells;
    buildCode();
  }
</script>

<style>
.lcd-col {
  display: flex;
  align-items: center;
  justify-content: center;
}

.lcd-cell {
  width: 24px;
  height: 24px;
  border: 1px solid #2d663e;
  background-color: #7ec089;
}

.lcd-cell-active {
  background-color: rgb(0, 0, 0);
}

.code {
}
</style>

<main>
  <section class="hero is-info">
    <div class="hero-body">
      <div class="container">
        <h1 class="title">
          LCD Custom Characters
        </h1>
      </div>
    </div>
  </section>

 <section class="section">
    <div class="container">
      <h1 class="title">Editor</h1>
      <h2 class="subtitle">
        You can use this editor to create your custom characters. After making your
        art piece, don't forget to create a Pull Request!
      </h2>

      <div class="columns">
        <div class="column is-one-third">
        {#each { length: 8 } as _, row}
          <div class="lcd-col">
            {#each { length: 5 } as _, col}
            <div 
              class="lcd-cell"
              class:lcd-cell-active="{cells[row][col]}"
              data-x="{col}"
              data-y="{row}"
              on:click={() => cellClicked(row, col)}
              ></div>
            {/each}  
          </div>
        {/each}
        </div>
         <div class="column code">
          <pre>
            {code}
          </pre>
         </div>
      </div>
      <div class="columns is-centered">
        <div class="column is-one-third">
          <button class="button is-info" on:click={clear}>Clear</button>
        </div>
      </div>
    </div>
  </section>

  <Library on:message={load} />

  <section class="section">
  <div class="container">
      <h1 class="title">Source</h1>
      <p><a href="https://github.com/tncardoso/lcd-custom-chars" target="_blank">Fork on Github</a></p>
  </div>
</section>
</main>
