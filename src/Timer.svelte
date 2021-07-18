<script>
  import { createEventDispatcher } from "svelte";
  import ProgressBar from "./ProgressBar.svelte";

  const totalSec = 3;
  let secondsLeft = totalSec;
  let isRunning = false;

  const dispatch = createEventDispatcher();

  function startTimer() {
    const timer = setInterval(() => {
      isRunning = true;
      secondsLeft -= 1;
      if (secondsLeft === 0) {
        clearInterval(timer);

        setTimeout(() => {
          isRunning = false;
          secondsLeft = totalSec;
          dispatch("end", "end timer");
        }, 1000);
      }
    }, 1000);
  }

  $: progress = ((totalSec - secondsLeft) / totalSec) * 100;
</script>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left: {secondsLeft}</h2>
</div>
<ProgressBar {progress} />
<div bp="grid">
  <button
    bp="offset-5@md 4@md 12@sm"
    class="start"
    disabled={isRunning}
    on:click={startTimer}
  >
    Start
  </button>
</div>

<style>
  h2 {
    margin: 0;
  }
  .start {
    background-color: darkred;
    width: 100%;
    margin: 10px 0;
  }
  .start[disabled] {
    background-color: lightgrey;
    cursor: not-allowed;
  }
</style>
