<script lang="ts">
    import Block from '$lib/components/block.svelte'

    const WIDTH = 20
    const HEIGHT = 20

    let board : Array<Array<'block' | 'segment' | 'fruit'>> = []

    function render() {
        board = []
        for (let i = 0; i < HEIGHT; i++) {
            const row : Array<'block' | 'segment' | 'fruit'> = []
            for (let j = 0; j < WIDTH; j++) {
                row.push('block')
            }
            board.push(row)
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