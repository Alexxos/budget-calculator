<script>
  import Title from "./Title.svelte";
  import Expense from "./Expense.svelte";
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  export let expenses = [];
</script>

<style>

</style>

<section>
  <Title title="Expense List" />
  {#each expenses as expense, index (expense.id)}
    <div 
    in:fly={{ x: 200, delay: index + 1 * 700 }}     out:fly={{ x: -200 }} animate:flip>
      <Expense {...expense} />
    </div>
  {:else}
    <p>No expenses added to the list</p>
  {/each}
</section>
