<script lang="ts">
    import Block from '$lib/components/block.svelte'

    const WIDTH = 30
    const HEIGHT = 30

    let board : Array<Array<'block' | 'segment' | 'fruit'>> = []

    const body = [{
        x : Math.floor(WIDTH / 2),
        y : Math.floor(HEIGHT / 2)
    }]

    function render() {
        board = []
        for (let i = 0; i < HEIGHT; i++) {
            const row : Array<'block' | 'segment' | 'fruit'> = []
            for (let j = 0; j < WIDTH; j++) {
                row.push('block')
            }
            board.push(row)
        }

        for (let segment of body) {
            board[segment.y][segment.x] = 'segment'
        }
    }
    render()
    

</script>

<div class="container">
    <div class="board">
        {#each board as row}
            {#each row as block}
                <div class="block-container">
                    <Block type={block}/>
                </div>
            {/each}
            <br>
        {/each}
    </div>
</div>

<style>
    .container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        widows: 100vw;
    }
    .block-container {
        display: inline-block;
        margin: 1px;
    }
</style>