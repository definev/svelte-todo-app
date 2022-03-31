<script lang="ts">
  let todos: {
    id: number;
    text: string;
    completed: boolean;
  }[] = [];

  function onAddTodo(event) {
    event.preventDefault();
    const value = event.target.value;
    event.target.value = '';
    todos = [
      ...todos,
      {
        id: todos.length,
        text: value,
        completed: false,
      },
    ];
  }

  function onComplete(todo: { id: number; text: string; completed: boolean }) {
    todos = todos.map((t) => {
      if (t.id === todo.id) {
        return {
          ...t,
          completed: true,
        };
      }
      return t;
    });
  }

  function onIncomplete(todo: {
    id: number;
    text: string;
    completed: boolean;
  }) {
    todos = todos.map((t) => {
      if (t.id === todo.id) {
        return {
          ...t,
          completed: false,
        };
      }
      return t;
    });
  }

  function onDeleteTodo(id: number) {
    todos = todos.filter((t) => t.id !== id);
  }
</script>

<main>
  <input
    on:change={onAddTodo}
    class="todo-input"
    type="text"
    placeholder="Nhập todo"
  />
  <div class="todo-content">
    {#each todos as { id, text, completed } (id)}
      <div class={completed ? 'complete' : 'incomplete'}>
        {text}
        <button
          class={completed ? 'complete-btn' : 'incomplete-btn'}
          on:click={() =>
            completed
              ? onIncomplete({ id, text, completed })
              : onComplete({ id, text, completed })}
          >{completed ? 'Not complete' : 'Complete'}</button
        >
        <div class="close-btn" on:click={() => onDeleteTodo(id)}>
          <span>X</span>
        </div>
      </div>
    {/each}
  </div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .todo-input {
    margin: auto;
    align-items: center;
    height: 50px;
    width: 360px;
    border-color: black;
    border-radius: 20px 10px 20px 10px;
    padding: 0 20px;
  }

  .todo-content {
    margin: auto;
    align-items: center;
  }

  .incomplete {
    position: relative;
    border-color: red;
    border: 2px solid red;
    height: 50px;
    width: 360px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin: 20px;
    padding: 0 8px 0 20px;
    border-radius: 20px 10px 20px 10px;
  }

  .incomplete-btn {
    background-color: greenyellow;
    color: chocolate;
    border: 0;
    padding: 10px 15px;
    border-radius: 15px 5px 15px 5px;
  }

  .complete {
    border: 2px solid green;
    height: 50px;
    width: 360px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin: 20px;
    padding: 0 8px 0 20px;
    border-radius: 20px 10px 20px 10px;
  }

  .complete-btn {
    background-color: red;
    color: white;
    border: 0;
    padding: 10px 15px;
    border-radius: 15px 5px 15px 5px;
  }

  .close-btn {
    height: 15px;
    width: 15px;
    background-color: red;
    border-radius: 50%;
    position: absolute;
    right: -7.5px;
    top: -7.5px;
    display: none;
    align-items: center;
    color: white;
    font-size: 9px;
    font-weight: 600;
    cursor: pointer;
  }

  .incomplete:hover .close-btn {
    display: block;
  }

  span {
    margin-left: 4.5px;
    line-height: 14px;
  }
</style>
