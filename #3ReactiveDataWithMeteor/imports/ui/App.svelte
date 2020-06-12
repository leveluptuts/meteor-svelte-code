<script>
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Resolutions } from "../api/resolutions";

  $: resolutions = useTracker(() => Resolutions.find({}).fetch());
</script>

<header>
  <h1>YO that's fresh</h1>
  {#each $resolutions as resolution}
    <h2>{resolution.title}</h2>
  {/each}
</header>
