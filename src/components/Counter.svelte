<script>
  import { writable } from "svelte/store";

  const storedCount = JSON.parse(localStorage.getItem("svelty"))?.count || 0;
  let count = writable(storedCount);
  count.subscribe(value => {
      localStorage.setItem("svelty", JSON.stringify({count: Number(value)}));
  });

  function add() {
    $count += 1;
  }

  function subtract() {
    $count -= 1;
  }
</script>

<div class="counter">
  <button on:click={subtract}>-</button>
  <pre>{ $count }</pre>
  <button on:click={add}>+</button>
</div>
<div class="message">
  <slot />
</div>

<style>
  .counter{
    display: grid;
    font-size: 2em;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    margin-top: 2em;
    place-items: center;
  }
  .message {
    text-align: center;
  }
</style>
