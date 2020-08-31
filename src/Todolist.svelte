<script lang="ts">
  let title = '';
  let todoList: string[] = [];

  $: disabledCreateButton = title === '';

  // 作成ボタンを押したときの処理
  const handleClickCreateButton = () => {
    todoList = [...todoList, title];
    title = '';
  };

  // 完了処理
  const completeItem = (index) => {
    todoList = todoList.filter((_, i) => i !== index);
  };
</script>

<div class="container mt-">
  <div class="row justify-content-center">
    <div class="col-lg-6 col-md-8">
      <h2>TODO アプリ</h2>
      <div class="form-group">
        <label for="title">タイトル</label>
        <input id="title" class="form-control" bind:value={title} />
      </div>
      <div class="form-group text-center">
        <button
          class="btn btn-primary px-5"
          disabled={disabledCreateButton}
          on:click={handleClickCreateButton}>
          作成
        </button>
      </div>
    </div>
  </div>
  <div class="row justify-content-center">
    <div class="col-lg-6 col-md-8">
      {#if todoList.length === 0}
        <div>アイテムを作成してください</div>
      {:else}
        <ul class="list-group">
          {#each todoList as todoItem}
            <li class="list-group-item align-middle">{todoItem}</li>
          {/each}
        </ul>
      {/if}
    </div>
  </div>
</div>
