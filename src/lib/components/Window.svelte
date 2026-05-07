<script>
    let { children, name, onClose, onMinimize, onMaximize } = $props();


    let x = $state(100);
    let y = $state(200);
    let isDragging = $state(false);

    let grabX = 0;
    let grabY = 0;
</script>

<svelte:window
    onpointermove={(e) => {
        if (isDragging) {
            x = e.clientX - grabX;
            y = e.clientY - grabY;
        }
    }}
    onpointerup={() => (isDragging = false)}
/>

<div class="window" style:left="{x}px" style:top="{y}px">
    {#if name}
        <div
            class="window-header"
            role="button"
            tabindex="0"
            onpointerdown={(e) => {
                isDragging = true;
                grabX = e.clientX - x;
                grabY = e.clientY - y;
            }}
        >
            <span class="window-title">{name}</span>
            <button class="window-close" onpointerdown={(e) => { onClose?.(e); }}>×</button>
            <button class="window-minimize" onpointerdown={(e) => { onMinimize?.(e); }}>−</button>
            <button class="window-maximize" onpointerdown={(e) => { onMaximize?.(e); }}>＋</button>
        </div>
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

    .window-header {
        background-color: #333;
        color: white;
        padding: 4px 8px;
        font-size: 12px;
        cursor: grab;
    }

    .window-title {
        display: block;
    }
</style>
