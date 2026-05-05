<script>
  let { children, name } = $props();

  let x = $state(100);
  let y = $state(200);
  let isDragging = $state(false);

  let grabX = 0;
  let grabY = 0;
</script>

<svelte:window 
  onmousemove={(e) => { if (isDragging) { x = e.clientX - grabX; y = e.clientY - grabY; } }}
  onmouseup={() => (isDragging = false)}
/>

<div 
  class="window"
  style:left="{x}px"
  style:top="{y}px"
  >
  {#if name}
    <div 
    class="window-title"
    role="button"
    tabindex="0"
    onmousedown={(e) => {
    isDragging = true;
    grabX = e.clientX - x;
    grabY = e.clientY - y;
  }}>{name}</div>
  {/if}
  {@render children?.()}
</div>

<style>
  .window {
    width: 100px;
    height: 100px;
    background-color: white;
    border: 1px solid #333;
    position: absolute;
    user-select: none;
  }
  
  .window-title {
    background-color: #333;
    color: white;
    padding: 4px 8px;
    font-size: 12px;
    cursor: grab;
  }
</style>