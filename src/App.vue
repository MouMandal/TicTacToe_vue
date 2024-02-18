<script setup>
import { ref, computed } from 'vue';
const player = ref("x");
const board = ref([
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
])
const checkWinner = (win) => {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
    ];
    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (win[a] && win[a] === win[b] && win[a] === win[c]) {
            return win[a];
        }
    }
    return null;
}
//To get the winner
const winner = computed(() => checkWinner(board.value.flat()));
const makeMove = (x, y) => {
    if (winner.value) {
        return;
    }
    if (board.value[x][y] !== '') {
        return;
    }
    board.value[x][y] = player.value;
    player.value = (player.value === 'x') ? 'o' : 'x';
}
//reset the game
const reset = () => {
    board.value = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
    ]
    player.value = 'x';
}
</script>
<template>
    <h1>TicTacToe using vue.js</h1>
    <h3>Player {{ player }} is turn</h3>
    <div class="container">
        <div v-for="(row, x) in board" :key="x" class="row">
            <div v-for="(cell, y) in row" :key="y" @click="makeMove(x, y)" class="row_1"><span class="boxtext">{{ cell
            }}</span>
            </div>
        </div>
    </div>
    <div class="button">
        <button @click="reset" id="btn">Reset</button>
    </div>
</template>




