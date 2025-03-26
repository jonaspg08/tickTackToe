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
      if (gameBoard.value[i][0] === gameBoard.value[i][1] && gameBoard.value[i][1] === gameBoard.value[i][2] && gameBoard.value[i][1] !=='') {
        return true;
      } else if (gameBoard.value[0][m] === gameBoard.value[1][m] && gameBoard.value[1][m] === gameBoard.value[2][m] && gameBoard.value[1][m] !=='') {
        return true;
      } else if (gameBoard.value[0][0] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][2] && gameBoard.value[1][1] !=='') {
        return true;
      } else if (gameBoard.value[0][2] === gameBoard.value[1][1] && gameBoard.value[1][1] === gameBoard.value[2][0] && gameBoard.value[1][1] !=='') {
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
  <main>
    <div v-for="(row, rowIndex) in gameBoard">
      <div v-for="(field, fieldIndex) in row">
        <button :class="field.toString()" @click="clickOnBoard(rowIndex, fieldIndex, activePlayer)">{{ field }}</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  display: flex;

}
button {
  width: 3rem;
  height: 3rem;
  font-size: 0.8rem;
  border: 1px solid black;
  background-color: white;
  cursor: pointer;
}

.true  {
  background-color: red;
}

.false {
  background-color: green;
}
</style>