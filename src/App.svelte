<script>
// import Github from './Github.svelte'
import GithubAwait from './GithubAwait.svelte'
  //components
  import { setContext, onMount, afterUpdate } from "svelte";
  // localStorage.setItem('testing','hello')
  import Navbar from "./Navbar.svelte";
  import ExpenseList from "./ExpenseList.svelte";
  import Title from "./Title.svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Modal from "./Modal.svelte";
  // Data
  // import expensesData from "./expenses";

  // variables
  let expenses = [];

  // set editing variables
  let setName = "";
  let setAmount = null;
  let setId = null;

  //  toggle form variables
  let isFormOpen = false;
  // reactive
  $: isEditing = setId ? true : false;
  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  //functions
  function showForm() {
    isFormOpen = true;
  }
  function hideForm() {
    isFormOpen = false;
    let setName = "";
    let setAmount = null;
    let setId = null;
  }
  function removeExpense(id) {
    expenses = expenses.filter(item => item.id !== id);
  }
  function clearExpenses() {
    expenses = [];
  }
  function addExpense({ name, amount }) {
    let expense = {
      id: Math.random() * Date.now(),
      name,
      amount
    };
    expenses = [expense, ...expenses];
  }
  function setModifiedExpense(id) {
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
  }
  function editExpense({ name, amount }) {
    expenses = expenses.map(item => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setName = "";
    setAmount = null;
  }

  // context
  setContext("remove", removeExpense);
  setContext("modify", setModifiedExpense);

  //local storage
  function setLocalStorage() {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  }
  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });
  afterUpdate(() => {
    console.log("something");
    setLocalStorage();
  });
</script>

<Navbar {showForm} />

<main class="content">
  {#if isFormOpen}
  <Modal>
    <ExpenseForm
      {addExpense}
      name={setName}
      amount={setAmount}
      id={setId}
      {isEditing}
      {editExpense}
      {hideForm} />
      </Modal>
  {/if}
  <Totals title="total expenses" {total} />
  <ExpenseList {expenses} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>
    clear expenses
  </button>
  
</main>
<!-- <Github/> -->
<GithubAwait/>