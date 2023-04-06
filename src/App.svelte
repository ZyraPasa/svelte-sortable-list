<script lang="ts">
  let items = ["item 1", "item 2", "item 3", "item 4", "item 5"];
  let activeDragIndex = -1;
  let activeDragEnterIndex = -1;
  const handleListDragOver = () => {
    if (activeDragEnterIndex !== activeDragIndex) {
      const item = items[activeDragIndex];
      items.splice(activeDragIndex, 1);
      items.splice(activeDragEnterIndex, 0, item);
      items = [...items];
      activeDragIndex = activeDragEnterIndex;
    }
  };
</script>

<div class="sortable-list">
  <ul on:dragover={handleListDragOver}>
    {#each items as item, index}
      <li
        data-index={index}
        draggable={true}
        class:active={activeDragIndex === index}
        on:dragstart={() => (activeDragIndex = index)}
        on:dragend={() => (activeDragIndex = -1)}
        on:dragenter={() => (activeDragEnterIndex = index)}
      >
        {item}
      </li>
    {/each}
  </ul>
</div>

<style lang="scss">
  .sortable-list {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #6670f0;
    display: grid;
    align-items: center;
    justify-content: center;
  }
  ul {
    width: 320px;
    border-radius: 1em;
    display: grid;
    user-select: none;
    grid-gap: 0.5em;
    background-color: #f9f9f9;
    padding: 1em;
    li {
      //   background-color: #f1f1f1;
      padding: 1em;
      //   border: 1px solid red;
      margin-top: 1px;
      width: 100%;
      cursor: move;
      display: grid;
      //   user-select: none;
    }
    .active {
      opacity: 0.5;
      box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    }
  }
</style>
