<script>
  const BOARD_SIZE = 9;
  const PLAYER_ICONS = { X: "O", O: "X" };
  const WIN_CONDITIONS = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];

  let buttons = new Array(BOARD_SIZE).fill(null);
  let result = null;
  let turnIcon = "X";
  let moveCount = 0;

  function setValue(buttonIndex) {
    buttons[buttonIndex] = turnIcon;
    buttons = [...buttons];
    turnIcon = PLAYER_ICONS[turnIcon];
    moveCount++;

    if (!buttons.includes(null)) {
      result = "Draw!";
    } else if (moveCount >= 5) {
      determineWinner();
    }
  }

  function determineWinner() {
    for (let i = 0; i < WIN_CONDITIONS.length; i++) {
      if (buttons[WIN_CONDITIONS[i][0]] != null) {
        if (
          buttons[WIN_CONDITIONS[i][0]] == buttons[WIN_CONDITIONS[i][1]] &&
          buttons[WIN_CONDITIONS[i][1]] == buttons[WIN_CONDITIONS[i][2]]
        ) {
          result = `${buttons[WIN_CONDITIONS[i][0]]} wins the game.`;
          break;
        }
      }
    }
  }

  function restart() {
    buttons = new Array(BOARD_SIZE).fill(null);
    result = null;
    turnIcon = "X";
    moveCount = 0;
  }
</script>

<main id="main">
  {#if !result}
    <h1>It is {turnIcon}'s turn.</h1>
    <div class="container">
      {#each buttons as button, buttonIndex}
        <button
          on:click={() => {
            setValue(buttonIndex);
          }}
          disabled={button !== null}
        >
          {button ? button : ""}
        </button>
      {/each}
    </div>
  {:else}
    <div class="result">
      <h1>{result}</h1>
      <button on:click={restart} class="restartBtn"> Restart Game </button>
    </div>
  {/if}
</main>
