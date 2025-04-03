<script>
  let listdata = [];
  let loading = true; 
  let error = null; // Initialize error state

  fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => {
          if (!response.ok) {
              throw new Error('Network response was not ok');
          }
          return response.json();
      })
      .then(results => {
          listdata = results;
          loading = false; 
      })
      .catch(err => {
          error = err.message; // Set error message
          loading = false; // Set loading to false on error
      });
</script>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <table class="table table-striped table-hover">
    <thead>
        <tr id="encabezado">
            <th>#</th>
            <th>Nombre</th>
            <th>Usuario</th>
            <th>Ciudad</th>
            <th>Email</th>
        </tr>
    </thead>
    <tbody>
      {#each listdata as values}
      <tr>
          <td>{values.id}</td>
          <td>{values.name}</td>
          <td>{values.username}</td>
          <td>{values.address.city}</td>
          <td>{values.email}</td>
      </tr>
      {/each}
    </tbody>
  </table>
{/if}

<style>
#encabezado {
  color: darkblue;
  background-color: rgb(23, 233, 93);
}
</style>
