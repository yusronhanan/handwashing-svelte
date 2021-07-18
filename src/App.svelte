<script>
  import Timer from "./Timer.svelte";
  import HowTo from "./HowTo.svelte";

  let audio;
  function timerEnds(e) {
    console.log(e);
    audio.play();
  }
</script>

<h1>Handwashing App</h1>
<Timer on:end={timerEnds} />

<HowTo />

<audio bind:this={audio}>
  <source src="ohyeah.wav" />
  <track kind="captions" />
</audio>

<style>
  h1 {
    text-align: center;
  }
</style>
