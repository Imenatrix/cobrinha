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

    let fruit : {x : number, y : number} | null = null

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

        if (fruit != null) {
            board[fruit.y][fruit.x] = 'fruit'
        }

        for (let segment of body) {
            board[segment.y][segment.x] = 'segment'
        }
    }

    let gameLoop = setInterval(() => {
        let head = body.at(-1)!

        if (
            head.x + movement.x >= 0 &&
            head.y + movement.y >= 0 &&
            head.x + movement.x <= WIDTH - 1 &&
            head.y + movement.y <= HEIGHT - 1
        ) {
            body.push({
                x : head.x + movement.x,
                y : head.y + movement.y
            })

            head = body.at(-1)!
            if (fruit != null) {
                if (head.x == fruit.x && head.y == fruit.y) {
                    fruit = null
                }
                else {
                    body.shift()
                }
            }
            else {
                body.shift()
            }

        }

        frootLoop: while (fruit == null) {
            let x = Math.floor(Math.random() * WIDTH)
            let y = Math.floor(Math.random() * HEIGHT)

            for (let segment of body) {
                if (segment.x == x && segment.y == y) {
                    continue frootLoop
                }
            }

            fruit = {
                x : x,
                y : y
            }
        }

        render()
    }, 500)

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