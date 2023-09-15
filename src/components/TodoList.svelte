
<script lang="ts">
  import {list, selection} from '../store/todo'
  import Button from './Button.svelte';
  import TodoAdd from './TodoAdd.svelte';
  import TodoItem from './TodoItem.svelte';

  const removeSelected = () => {
    $selection.forEach(list.remove)
  }

</script>

<div class="container">

  <h1 class="title">
    TODO
  </h1>
</div>
  
<header class="header">
  <TodoAdd/>

  {#if $list.length}
  <div>
    <Button disabled={!$selection.length} on:click={removeSelected} type="danger">
      Remove
      {#if $selection.length}
        ({$selection.length})
      {/if}  
    </Button>
    
    <Button on:click={list.removeAll} type="danger">
      Remove all
      ({ $list.length })
    </Button>
  </div>
  {/if}
  
</header>

{#if $list.length}
{#each  $list as item }
  <TodoItem {item}/>
{/each}
{:else}
  <div class="empty">
    Пусто
  </div>
{/if}

<style lang="scss">
  .title {
    font-size: 100px;
    margin: 0;
    text-align: center; /* Центрируйте заголовок */
    color: white; /* Установите цвет текста заголовка */
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); /* Добавьте тень тексту */
  }

  .header {
    display: flex;
    justify-content: space-between;
    background: linear-gradient(45deg, #ff8a00, #e52e71, #ff006c); /* Добавьте градиентный фон для хедера */
    padding: 20px; /* Увеличьте внутренний отступ хедера */
  }

  .empty {
    font-size: 20px;
    margin: 40px 0;
    text-align: center;
    border-top: 1px solid rgba(#000, 0.1);
  }
  
  body {
    background: linear-gradient(45deg, #ff8a00, #e52e71, #ff006c);
    background-size: 400% 400%;
    animation: gradientAnimation 10s ease infinite; /* Добавьте анимацию */
  }

  @keyframes gradientAnimation {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }
</style>
