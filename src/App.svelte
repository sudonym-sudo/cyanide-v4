<script>
  import Window from './lib/components/Window.svelte';
  // @ts-ignore
  let windows = $state([]);
  let context = $state('Nothing is happening...');
</script>

<section class="apps">
  <button class="apps-button" id="cyanide"
  onmouseenter={() => context = 'Launch cyanide'}
  onmouseleave={() => context = 'Nothing is happening...'}
  onclick={() => windows.push({ 
    id: crypto.randomUUID(),
    type: 'cyanide'
    })}
  >
    cyanide
  </button>
  <button class="apps-button" id="sulfur"
  onmouseenter={() => context = 'Launch sulfur'}
  onmouseleave={() => context = 'Nothing is happening...'}
  onclick={() => windows.push({
     id: crypto.randomUUID(),
     type : 'sulfur'
    })}
  >
    sulfur
  </button>
  <button class="apps-button" id="fluoride"
  onmouseenter={() => context = 'Launch fluoride'}
  onmouseleave={() => context = 'Nothing is happening...'}
  onclick={() => windows.push({ 
    id: crypto.randomUUID(),   
    type: 'fluoride'
    })}
  >
    fluoride
  </button>
</section>

{#each windows as window}
  {#if window.type === 'cyanide'}
    <Window name="Cyanide">
      <h1>Cyanide</h1>
    </Window>
  {:else if window.type === 'sulfur'}
    <Window name="Sulfur">
      <h1>Sulfur</h1>
    </Window>
  {:else if window.type === 'fluoride'}
    <Window name="Fluoride">
      <h1>Fluoride</h1>
    </Window>
    
  {/if}
{/each}

<section class="context">
  {context}
</section>

<style>
  .apps {
    display: flex;
    gap: 2rem;
    margin-left: 4rem;
    margin-top: 4rem;
    margin-bottom: 2rem;
  }

  .apps-button {
    border-radius: 20px;
    width: 5rem;
    height: 5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  #cyanide {
    background-color: cyan;
  }

  #sulfur {
    background-color: yellow;
  }

  #fluoride {
    background-color: greenyellow;
  }

  .context {
    margin-left: 4rem;
  }
</style>