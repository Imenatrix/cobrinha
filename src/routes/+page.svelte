<script lang="ts">
    import Block from '$lib/components/block.svelte'
    import { onDestroy, onMount } from 'svelte';

    const WIDTH = 30
    const HEIGHT = 30

    let board : Array<Array<'block' | 'segment' | 'fruit'>> = []

    const movement = {
        x : 1,
        y : 0
    }

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

    let gameLoop = setInterval(() => {
        let head = body.at(-1)!

        if (
            head.x > 0 &&
            head.y > 0 &&
            head.x < WIDTH - 1 &&
            head.y < HEIGHT - 1
        ) {
            head.x += movement.x
            head.y += movement.y
        }

        render()
    }, 1000)

    onMount(async () => {
        document.addEventListener('keydown', (event) => {
            if (event.key == 'ArrowUp') {
                movement.x = 0
                movement.y = -1
            }
            if (event.key == 'ArrowDown') {
                movement.x = 0
                movement.y = 1
            }
            if (event.key == 'ArrowRight') {
                movement.x = 1
                movement.y = 0
            }
            if (event.key == 'ArrowLeft') {
                movement.x = -1
                movement.y = 0
            }
            console.log(event.key)
        })
    })

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