<script lang="ts">
    import Block from '$lib/components/block.svelte'

    const WIDTH = 20
    const HEIGHT = 20

</script>

<div class="container">
    <div class="board">
        {#each new Array(HEIGHT) as row}
            {#each new Array(WIDTH) as block}
                <div class="block-container">
                    <Block />
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