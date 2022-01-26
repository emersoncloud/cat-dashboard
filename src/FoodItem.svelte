<script>
  export let amount;
  export let lastFed;
  import { format } from "date-fns";
  let src = amount === 0.5 ? "/can.png" : "/can-colored.png";
</script>

<div class="flex">
  <img {src} alt="can" />
  <span>{format(lastFed, "hh:mm do")}</span>
</div>

<style>
  img {
    height: 50px;
  }
  .flex {
    align-items: center;
    display: flex;
    justify-content: space-evenly;
  }
</style>
