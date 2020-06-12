<script>
  export let resolution;
  import { Resolutions } from "../../api/resolutions";
  let updateRes = resolution.title;

  function deleteRes() {
    Resolutions.remove(resolution._id);
  }

  function handleSubmit(event) {
    Resolutions.update(
      {
        _id: resolution._id
      },
      {
        title: updateRes
      }
    );
  }
</script>

<li>
  <form on:submit|preventDefault={handleSubmit}>
    <input type="text" bind:value={updateRes} />
    <button>Submit</button>
  </form>
  <button on:click={deleteRes}>Delete</button>

</li>
