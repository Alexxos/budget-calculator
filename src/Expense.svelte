<script>
import { getContext} from 'svelte';
import {blur, slide,scale,fade,fly} from 'svelte/transition';
import {quintOut} from 'svelte/easing'

  export let id;
  export let name;
  export let amount;

  let displayAmount = false;

//context
	const removeExpense = getContext('remove');
	const setModifiedExpense = getContext('modify');
</script>

<style>
  
</style>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={() => displayAmount=!displayAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if  displayAmount}
    <!-- <h4 transition:blur>amount : ${amount}</h4> -->
    <!-- <h4 transition:scale>amount : ${amount}</h4> -->
    <!-- <h4 transition:slide>amount : ${amount}</h4> -->
    <!-- <h4 transition:fade>amount : ${amount}</h4> -->
    <!-- <h4 in:fly={{x:-150,y:0,duration:2000,   delay:500, easing:quintOut}}
            out:slide> amount : ${amount}</h4> -->
      <h4 transition:slide>amount: ${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={setModifiedExpense(id)} >
      <i class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn" on:click={removeExpense(id)}>
      <i class="fas fa-trash" />
    </button>
  </div>
</article>
