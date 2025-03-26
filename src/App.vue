<script setup>
import { ref } from 'vue'

const gameBoard = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', '']
]);

function clickOnBoard(row, col, player) {
  if (gameBoard.value[row][col] === '') {
    gameBoard.value[row][col] = player;
  }

  console.log('winCheck', winCheck())
  activePlayer.value = !activePlayer.value;
}
const activePlayer = ref(false);

function winCheck() {
  for (let i = 0; i < gameBoard.value.length; i++) {
    for (let m = 0; m < gameBoard.value[i].length; m++) {
      if (gameBoard.value[i][0] === gameBoard.value[i][1] && gameBoard.value[i][1] === gameBoard.value[i][2] && gameBoard.value[i][1] !== '') {
        return true;
      } else if (gameBoard.value[0][m] === gameBoard.value[1][m] && gameBoard.value[1][m] === gameBoard.value[2][m] && gameBoard.value[1][m] !== '') {
        return true;
      } else if (gameBoard.value[0][0] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][2] && gameBoard.value[1][1] !== '') {
        return true;
      } else if (gameBoard.value[0][2] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][0] && gameBoard.value[1][1] !== '') {
        return true;
      }
    }
  } return false;
}

// if (gameBoard.value[0][0] === gameBoard.value[0][1] && gameBoard.value[0][1] === gameBoard.value[0][2] && gameBoard.value[0][1] !='') {
//   return true;
// } else if (gameBoard.value[1][0] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[1][2] && gameBoard.value[1][1] !='') {
//   return true;
// } else if (gameBoard.value[2][0] === gameBoard.value[2][1] && gameBoard.value[2][1] === gameBoard.value[2][2] && gameBoard.value[2][1] !='') {
//   return true;
// } else if (gameBoard.value[0][0] === gameBoard.value[1][0] && gameBoard.value[1][0] === gameBoard.value[2][0] && gameBoard.value[1][0] !='') {
//   return true;
// } else if (gameBoard.value[0][1] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][1] && gameBoard.value[1][1] !='') {
//   return true;
// } else if (gameBoard.value[0][2] === gameBoard.value[1][2] && gameBoard.value[1][2] === gameBoard.value[2][2] && gameBoard.value[1][2] !='') {
//   return true;
// } else if (gameBoard.value[0][0] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][2] && gameBoard.value[1][1] !='') {
//   return true;
// } else if (gameBoard.value[0][2] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][0] && gameBoard.value[1][1] !='') {
//   return true;
// } else {
//   return false;
// }


function resetGame() {
  gameBoard.value = [
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
  ];
}

</script>

<template>
  <div class="title">
    <h1>TickTackToe</h1>
  </div>
  <main>
    <div v-for="(row, rowIndex) in gameBoard">
      <div v-for="(field, fieldIndex) in row">
        <button :class="field.toString()" @click="clickOnBoard(rowIndex, fieldIndex, activePlayer)">
          <svg v-if="field === false" width="2rem" height="2rem" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="40" stroke="white" stroke-width="10" fill="none" />
          </svg>
          <svg v-if="field === true" width="2rem" height="2rem" viewBox="0 0 100 100">
            <line x1="10" y1="10" x2="90" y2="90" stroke="white" stroke-width="10" />
            <line x1="90" y1="10" x2="10" y2="90" stroke="white" stroke-width="10" />
          </svg>
        </button>
      </div>
    </div>
  </main>
  <button class="reset" @click="resetGame()">Reset Game</button>
</template>

<style scoped>
main {
  display: flex;
  margin-left: 45.5%;
}

.title {
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
}

button {
  width: 3rem;
  height: 3rem;
  font-size: 0.8rem;
  border: 1px solid black;
  background-color: white;
  cursor: pointer;
}

.true {
  background-color: red;
}

.false {
  background-color: green;
}

.reset {
  display: flex;
  margin-left: 47.4%;
  margin-top: 3rem;
  width: 90px;
  height: 20px;
  justify-content: center;
  border-radius: 5px;
  transition: all 1s;
  box-shadow: #9f9fad;
  background-color: #9f9fad;
}

.reset:hover{
background-color: #aecfdf;
color: #000000;
}
</style>