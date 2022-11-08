<script>
  import fetchJson from "../public/analyzer-result.json";
  import PackagesList from "./PackagesList.svelte";
  import Navbar from "./Navbar.svelte";
  let projectid = JSON.stringify(
    fetchJson.analyzer.result.projects[0].id
  ).replace(/\"/g, "");
  let packages = fetchJson.analyzer.result.packages;
  let files = [];
</script>

<Navbar />
<main class="content">
  <!-- <input type="file" bind:files accept="application/JSON" /> -->

  <div>
    Project id:
    <h4>
      {projectid}
    </h4>
  </div>

  <PackagesList {packages} />
</main>
