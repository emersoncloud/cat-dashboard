<script>
  import { formatDistance, getDayOfYear, addDays } from "date-fns";
  import FoodItem from "./FoodItem.svelte";
  const HALF_CAN = 0.5;
  const FULL_CAN = 1;
  const CAN_GOAL = 2.5;

  let lastFed = Date.now();
  let lastFedFriendly = formatDistance(lastFed, new Date(), {
    addSuffix: true,
  });
  let cansFed = 0;
  let foodEntries = [];

  function feedCan(amount) {
    cansFed += amount;
    foodEntries = [
      {
        amount,
        lastFed,
      },
      ...foodEntries,
    ];
    lastFed = Date.now();
  }
  setInterval(() => {
    lastFedFriendly = formatDistance(lastFed, new Date(), { addSuffix: true });
    if (getDayOfYear(lastFed) !== getDayOfYear(Date.now())) {
      cansFed = 0;
    }
  }, 1000 * 60);
</script>

<div class="body" />

<div class="hero-time">
  Last fed {lastFedFriendly}
</div>

<div class="flex">
  <div class="food-button" on:click={() => feedCan(FULL_CAN)}>
    <img id="half-can" alt="cat food can colored in" src={"/can-colored.png"} />
    <span class="food-text">Full Can</span>
  </div>
  <div class="food-button" on:click={() => feedCan(HALF_CAN)}>
    <img id="full-can" alt="cat food can outline" src={"/can.png"} />
    <span class="food-text">Half Can</span>
  </div>
</div>

<div class="food-total">
  <div class="display-text">Food so far today: {cansFed}</div>
  <div class="display-text" class:goal={cansFed >= CAN_GOAL}>
    Goal: {CAN_GOAL}
  </div>
  <div class="food-list">
    {#each foodEntries as { lastFed, amount } (lastFed)}
      <FoodItem {lastFed} {amount} />
    {/each}
  </div>
</div>

<style>
  .display-text {
    font-size: 1.2em;
  }
  .goal {
    background-color: rgb(108, 233, 104);
  }
  .food-list {
    width: 300px;
    height: 200px;
    overflow-y: scroll;
  }
  .food-button {
    cursor: pointer;
    display: flex;
    flex-direction: column;
  }
  .hero-time {
    text-align: center;
    font-size: 5em;
  }
  .food-text {
    text-align: center;
    font-size: 2em;
  }

  .food-total {
    font-size: 2em;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
  }

  #half-can,
  #full-can {
    height: 20vh;
  }
  #one {
    color: blue;
  }

  #heading {
    display: flex;
    justify-content: center;
  }
  .body {
    background-image: url("/puddle.png");
    background-repeat: repeat;
    background-size: 50px 50px;
    opacity: 20%;
    position: absolute;
    height: 100vh;
    width: 100vw;
    z-index: -1;
  }

  .flex {
    margin: 16px;
    display: flex;
    justify-content: space-evenly;
  }
</style>
