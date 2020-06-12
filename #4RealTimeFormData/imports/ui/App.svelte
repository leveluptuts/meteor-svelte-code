<script>
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Resolutions } from "../api/resolutions";

  let newRes = "";

  $: resolutions = useTracker(() => Resolutions.find({}).fetch());

  function handleSubmit(event) {
    Resolutions.insert({
      title: newRes
    });

    newRes = "";
  }
</script>

<header>
  <h1>YO that's fresh</h1>

  <form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="Add your resolution" bind:value={newRes} />
    <button>Submit</button>
  </form>

  {#each $resolutions as resolution}
    <h2>{resolution.title}</h2>
  {/each}
</header>
