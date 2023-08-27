<script>
  let buttons = new Array(9).fill(null);
  let result = null;
  let turnIcon = 'X'

  function setValue(i) {
    buttons[i] = turnIcon;
    buttons = [...buttons]
    turnIcon = turnIcon == "X" ? "O" : 'X'
  }
</script>

{#if !result}
  <div class="container">
    {#each buttons as button, i}
      <button on:click={() => {setValue(i)}}>
        {button ? button: ""}
      </button>
    {/each}
  </div>
{:else}

{/if}