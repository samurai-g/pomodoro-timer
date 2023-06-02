<script>
  import { onMount } from "svelte";

  export let timerDurationMinutes = 25; //typically 25 minutes

  let timerDurationSeconds = timerDurationMinutes * 60; // minutes in seconds
  let timeLeft = timerDurationSeconds;
  let timer;

  //editable timer with input fields
  let minutesLeft = Math.floor(timeLeft / 60);
  let secondsLeft = timeLeft % 60;

  //reactive statement
  $: {
    minutesLeft = Math.floor(timeLeft / 60);
    secondsLeft = (timeLeft % 60).toString().padStart(2, "0"); //thanks ChatGPT for padStart
  }

  function updateTime() {
    timeLeft = parseInt(minutesLeft) * 60 + parseInt(secondsLeft);
  }

  let timerRunning = false;
  let timerColor = "#79f35b";

  function toggleTimer() {
    if (timerRunning) {
      pauseTimer();
    } else {
      startTimer();
    }
  }

  function startTimer() {
    timerRunning = true;
    if (!timer) {
      timerColor = "#f3a053";
      timer = setInterval(() => {
        if (timeLeft > 0) {
          timeLeft--;
        } else {
          clearInterval(timer);
          timer = null;
          alert("Time is up!");
        }
      }, 1000);
    }
  }

  function pauseTimer() {
    timerRunning = false;
    if (timer) {
      clearInterval(timer);
      timerColor = "#79f35b";
      timer = null;
    }
  }

  //reset to 25 minutes (standard)
  function resetTimer() {
    pauseTimer();
    timeLeft = timerDurationSeconds;
  }

  function addFiveMinutes() {
    timeLeft += 5 * 60;
  }
</script>

<div>
  <!--Time left: {Math.floor(timeLeft / 60)}:{(timeLeft % 60).toString().padStart(2, '0')}-->
  <input type="number" min="0" bind:value={minutesLeft} on:input={updateTime} />
  :
  <input
    type="number"
    min="0"
    max="59"
    bind:value={secondsLeft}
    on:input={updateTime}
  />
</div>
<div class="timerButtons">
  <button on:click={toggleTimer}>{timerRunning ? "PAUSE" : "START"}</button>
  <button on:click={resetTimer}>RESET</button>
  <button on:click={addFiveMinutes}>+5 MIN</button>
</div>

<style>
  input {
    width: 4em;
    text-align: center;
    border-radius: 5px;
  }

  div {
    text-align: center;
    padding: 0.5em;
    max-width: 220px;
    margin: 0 auto;
  }

  .timerButtons {
    padding: 0;
  }

  button {
    background-color: rgb(209, 213, 219, 0.5);
    border: 1px solid rgb(186, 189, 194);
    border-radius: 0.5rem;
    box-sizing: border-box;
    color: white;
    font-size: 0.875rem;
    font-weight: 500;
    line-height: 1rem;
    padding: 0.75rem 1rem;
    text-align: center;
    text-decoration: none #d1d5db solid;
    text-decoration-thickness: auto;
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
    cursor: pointer;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
  }

  button:hover {
    background-color: rgb(209, 213, 219, 0.9);
  }

  button:focus {
    outline: 2px solid transparent;
    outline-offset: 2px;
  }

  button:focus-visible {
    box-shadow: none;
  }
</style>
