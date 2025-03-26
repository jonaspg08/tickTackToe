<script setup>
import { ref } from 'vue'
import PageOverlay from './components/PageOverlay.vue'

const gameBoard = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', '']
]);

function clickOnBoard(row, col, player) {
  if (gameBoard.value[row][col] === '' && !gameOver.value) {
    gameBoard.value[row][col] = activePlayer.value;
  }
  if (gameEnd()) return;
  console.log('winCheck', winCheck())
  activePlayer.value = !activePlayer.value;
}
const activePlayer = ref(false);
const gameOver = ref(false);

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

function isBoardFull() {
  return gameBoard.value.every(row => row.every(cell => cell !== ''))
}

function gameEnd() {
  if (winCheck()) {
    gameOver.value = true;
    return true;
  } else if (isBoardFull()) {
    gameOver.value = true;
    return true;
  }
  return false;
}

function resetGame() {
  gameOver.value = false;
  gameBoard.value = [
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
  ];
}
</script>

<template>
  <div class="title">
    <p>TickTackToe</p>
  </div>
  <main>
    <div v-for="(row, rowIndex) in gameBoard">
      <div v-for="(field, fieldIndex) in row">
        <button :class="field.toString()" @click="clickOnBoard(rowIndex, fieldIndex, activePlayer)">
          <svg v-if="field === false" width="12rem" height="12rem" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="40" stroke="red" stroke-width="10" fill="none" />
          </svg>
          <svg v-if="field === true" width="12rem" height="12rem" viewBox="0 0 100 100">
            <line x1="10" y1="10" x2="90" y2="90" stroke="green" stroke-width="10" />
            <line x1="90" y1="10" x2="10" y2="90" stroke="green" stroke-width="10" />
          </svg>
        </button>
      </div>
    </div>
  </main>
  <button class="reset" @click="resetGame()">Reset Game</button>
  <PageOverlay :gameBoard="gameBoard"/>
</template>
<style scoped></style>