<script>
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Resolutions } from "../api/resolutions";
  import { LoginWindow, Logout } from "meteor/levelup:svelte-accounts-ui";
  import Resolution from "./resolutions/Resolution.svelte";
  let newRes = "";

  $: resolutions = useTracker(() => Resolutions.find({}).fetch());
  $: userId = useTracker(() => Meteor.userId());

  function handleSubmit(event) {
    Resolutions.insert({
      title: newRes
    });

    newRes = "";
  }
</script>

<header>
  <h1>YO that's fresh</h1>

  {#if $userId}
    <Logout />
  {:else}
    <LoginWindow />
  {/if}

  <form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="Add your resolution" bind:value={newRes} />
    <button>Submit</button>
  </form>
</header>

{#each $resolutions as resolution}
  <Resolution {resolution} />
{/each}
