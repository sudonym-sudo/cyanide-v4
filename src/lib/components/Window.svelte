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
            <button
                class="window-close"
                onclick={(e) => {
                    e.stopPropagation();
                    onClose?.(e);
                }}>×</button
            >
            <button
                class="window-minimize"
                onclick={(e) => {
                    e.stopPropagation();
                    onMinimize?.(e);
                }}>−</button
            >
            <button
                class="window-maximize"
                onclick={(e) => {
                    e.stopPropagation();
                    onMaximize?.(e);
                }}>＋</button
            >
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
        display: flex;
        align-items: center;
        gap: 8px;
    }

    .window-title {
        flex: 1;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .window-header button {
        background: none;
        border: none;
        color: white;
        padding: 0 4px;
        cursor: pointer;
        font-size: 14px;
        line-height: 1;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .window-header button:hover {
        background-color: #555;
    }

    .window-close:hover {
        background-color: #e81123 !important;
    }
</style>
