<script>
  let { children } = $props();

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
  role="button"
  tabindex="0"
  style:left="{x}px"
  style:top="{y}px"
  onmousedown={(e) => {
    isDragging = true;
    grabX = e.clientX - x;
    grabY = e.clientY - y;
  }}>
  {@render children?.()}
</div>

<style>
  .window {
    width: 100px;
    height: 100px;
    background-color: white;
    border: 1px solid #333;
    position: absolute;
    cursor: grab;
    user-select: none;
  }
</style>