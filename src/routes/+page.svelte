<script lang="ts">

    let grid: string[][] = [];
    for (let i = 0; i < 3; i++) {
        grid.push([]);
        for (let j = 0; j < 3; j++) {
            grid[i].push(' ');
        }
    }

    let currentPlayer = 'X';

    function addMarker(i: number, j: number) {
        if (grid[i][j] !== ' ') {
            return
        }
        grid[i][j] = currentPlayer;
        checkWinner(i, j);
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }

    function checkWinner(i: number, j: number) {
        let row = grid[i].join('');
        let col = grid.map(row => row[j]).join('');
        let diag1 = grid.map((row, idx) => row[idx]).join('');
        let diag2 = grid.map((row, idx) => row[2 - idx]).join('');
        if (row === 'XXX' || col === 'XXX' || diag1 === 'XXX' || diag2 === 'XXX') {
            alert('X wins');
            reset();
        } else if (row === 'OOO' || col === 'OOO' || diag1 === 'OOO' || diag2 === 'OOO') {
            alert('O wins');
            reset();
        }
    }

    function reset() {
        grid = grid.map(row => row.map(() => ' '));
    }

</script>

<div class="flex">
    {#each grid as row, i}
        <div class="">
            {#each row as cell, j}
                <div class="border p-5 w-16 h-16" on:click={() => addMarker(i, j)}>
                    {grid[i][j]}
                </div>
            {/each}
        </div>
    {/each}
</div>

<style lang="scss">
  @import "tailwindcss";
</style>