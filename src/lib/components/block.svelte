<script lang="ts">
    export let type : 'block' | 'segment' | 'fruit' = 'block'
</script>

<div class="block"
    class:segment={type === 'segment'}
    class:fruit={type === 'fruit'}
></div>

<style>
    .block {
        width: 30px;
        height: 30px;
        background-color : gray;
        display: inline-block;
        vertical-align: top;
    }
    .segment {
        background-color : green;
    }
    .fruit {
        background-color : red;
    }
</style>