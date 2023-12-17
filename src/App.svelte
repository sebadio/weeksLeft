<script lang="ts">
  import { onMount } from "svelte";

  const weeks: boolean[] = new Array(3650).fill(false);
  const today = new Date();
  // date of 29/01/2003
  const startDate = new Date(2003, 0, 29);
  // calculate the number of weeks between the start date and today
  const weeksSinceStart = Math.floor(
    (today.getTime() - startDate.getTime()) / (1000 * 60 * 60 * 24 * 7)
  );
  console.log(weeksSinceStart);

  // set the weeks since start to true
  for (let i = 0; i < weeksSinceStart; i++) {
    weeks[i] = true;
  }
</script>

<main>
  <h1>Memento Mori</h1>
  <p>
    The red squares represent the weeks you have lived. The white squares
    represent the weeks you have left.
    <br />
    <br />
    Remember that you will die.
  </p>

  <div class="holder">
    {#each weeks as week, index}
      {#if week}
        <div
          class="week filled"
          style="transition-delay: {index}s; opacity: 1;"
        ></div>
      {:else}
        <div class="week" style="transition-delay: {index}s; opacity: 1;"></div>
      {/if}
    {/each}
  </div>
</main>

<style>
  .holder {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 100%;
    max-width: 50%;
    margin: 0 auto;
    gap: 2px;
  }

  .week {
    width: 0.6rem;
    height: 0.6rem;
    background-color: white;
    border-radius: 1px;
    transition: opacity 0.2s cubic-bezier(0.215, 0.61, 0.355, 1);
    opacity: 0;
  }

  .filled {
    background-color: rgb(233, 114, 114);
  }
</style>
