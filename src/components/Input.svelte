<script lang="ts">
    import { createEventDispatcher } from "svelte";

    export let value = '';

    export let placeholder = '';

    const dispatch = createEventDispatcher();

    const onInput = (event:any) => {
        value = event.target.value;
    }

    const onKeyDown = (event:KeyboardEvent) => {
        if (event.code === 'Enter') {
            dispatch('enter');
        }
    }
</script>

<input class="input" type="text" {value} {placeholder} on:input={onInput} on:keydown={onKeyDown}>

<style lang="scss">
    .input {
        padding: 10px 20px;
        border: 1px solid rgba(#000, 0.1);
        border-radius: 5px;
        outline: none;
    }
</style>