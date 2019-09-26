<script>

export let playerIndex = 1; // 1 or 2;

// 0 = not filled
// 1 = player 1 filled
// 2 = player 2 filled

const board = [
  [0,0,0,0,0,0,0],  // row 0
  [0,0,0,0,0,0,0],  // row 1
  [0,0,0,0,0,0,0],  // row 2
  [0,2,0,0,0,0,0],  // row 3
  [0,2,2,0,0,0,0],  // row 4
  [1,1,1,2,0,0,0],  // row 5
]

const addStoneToColumn = (itemIndex, playerIndex) => {
  const numberOfRows = board.length;

  let lastRow = -1;
  for (let rowIndex = 0; rowIndex < numberOfRows; rowIndex++) {
    if (board[rowIndex][itemIndex] === 0){
      lastRow = rowIndex;
    }
  }

  if(lastRow !== -1) {
    board[lastRow][itemIndex] = playerIndex;
  } else {
    // Should not come here.
    alert('already placed');
  }
}

const itemClickHandler = (rowIndex, columnIndex) => {
  if (board[rowIndex][columnIndex] === 0) {
    const currentPlayerIndex = playerIndex === 1 ? 1 : 2;
  
    addStoneToColumn(columnIndex, currentPlayerIndex);
  
    playerIndex = currentPlayerIndex === 1 ? 2 : 1;
  } else {
    alert('Already filled');
  }
}

</script>


<style>

.board {
  background-color: #444;
  color: #fff;
  border-radius: 5px;
  padding: 20px;
}

.grid {
  width: 800px;
  margin: 0 auto;

  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-gap: 1em;
}

.item {
  background-color: azure;
  color: black;

  height: 50px;
  width: 50px;
  padding: 20px;
  border-radius: 50%;
}

.item--hover-playerx:hover {
  background-color: limegreen;
  cursor: pointer;
}

.item--hover-playery:hover {
  background-color: powderblue;
  cursor: pointer;
}

.playerx {
  background-color: darkgreen;
}

.playery {
  background-color: rgba(49, 74, 156, 0.575);
}

</style>
<div class="board">
  <div class="grid">
    {#each board as row, rowIndex}
      {#each row as item, columnIndex}
        <div 
            class="item"
            class:item--hover-playerx="{playerIndex === 1 && item === 0}"
            class:item--hover-playery="{playerIndex === 2 && item === 0}"
            class:item--hover="{item === 0}"
            class:playerx="{item === 1}"
            class:playery="{item === 2}"
            on:click={() => itemClickHandler(rowIndex, columnIndex)}>
        </div>
      {/each}
    {/each}
  </div>
</div>