<script>
  import SectionTitle from "./Title.svelte";
  import Package from "./Package.svelte";
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  import App from "./App.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  export let packages = [];
</script>

<section>
  <SectionTitle title="Package list" />
  <ul>
    {#each packages as package_, index (JSON.stringify(package_.metadata.id))}
      <div
        in:fly={{ x: 200, delay: (index + 1) * 700 }}
        out:fly={{ x: -200 }}
        animate:flip
      >
        <Package {package_} id={index + 1} />
      </div>
    {:else}
      <h2>no packages added to the list</h2>
    {/each}
  </ul>
</section>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
