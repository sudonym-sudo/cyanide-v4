<script>
  import Window from './lib/components/Window.svelte';
  let context = $state('Nothing is happening...');
</script>

<section class="apps">
  <button class="apps-button" id="cyanide"
  onmouseenter={() => context = 'Launch cyanide'}
  onmouseleave={() => context = 'Nothing is happening...'}
  >
    cyanide
  </button>
  <button class="apps-button" id="sulfur"
  onmouseenter={() => context = 'Launch sulfur'}
  onmouseleave={() => context = 'Nothing is happening...'}
  >
    sulfur
  </button>
  <button class="apps-button" id="fluoride"
  onmouseenter={() => context = 'Launch fluoride'}
  onmouseleave={() => context = 'Nothing is happening...'}
  >
    fluoride
  </button>
</section>

<Window>
  <!-- Window content goes here -->
</Window>

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