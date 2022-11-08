<script>
  import { blur, slide, scale, fade, fly } from "svelte/transition";
  import { quintOut } from "svelte/easing";
  import { getContext } from "svelte";
  export let package_;
  export let metadata = "";
  export let curations = [];
  export let id;
  export let name = JSON.stringify(package_.metadata.id).replace(/\"/g, "");
  export let amount = JSON.stringify(package_.metadata.declared_licenses[0]);
  if (amount) {
    amount = amount.replace(/\"/g, "");
  }
  export let desc = JSON.stringify(package_.metadata.description).replace(
    /\"/g,
    ""
  );
  export let homepage_url = JSON.stringify(
    package_.metadata.homepage_url
  ).replace(/\"/g, "");
  let displayAmount = false;

  function toggleAmount() {
    displayAmount = !displayAmount;
  }

  const removeExpense = getContext("remove");
  const setModifiedExpense = getContext("modify");
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {id}. {name}
      <button class="amount-btn" on:click={toggleAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if displayAmount}
      <!-- <h4 transition:blur>amount : ${amount}</h4> -->
      <!-- <h4 transition:scale>amount : ${amount}</h4> -->
      <!-- <h4 transition:slide>amount : ${amount}</h4> -->
      <!-- <h4 transition:fade>amount : ${amount}</h4> -->
      <p>License:</p>
      <h4 transition:slide>{amount}</h4>
      <p>Homepageurl:</p>
      <h4 transition:slide>{homepage_url}</h4>
      <p>description:</p>
      <h4 transition:slide>{desc}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button
      class="expense-btn edit-btn"
      on:click={() => setModifiedExpense(id)}
    >
      <i class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}>
      <i class="fas fa-trash" />
    </button>
  </div>
</article>
