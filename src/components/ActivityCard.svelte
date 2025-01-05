<script>
  export let unit;
  export let onClick;
</script>

<div class="activity-card" on:click={() => onClick(unit)}>
  <h3>{unit.name}</h3>
  <p>{unit.description}</p>
</div>

<style>
  .activity-card {
    margin: 1rem 0;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 5px;
    transition:
      background-color 0.3s,
      border-color 0.3s;
    cursor: pointer;
  }

  :global(body.dark-mode) .activity-card {
    border-color: #444;
    background-color: #2a2a2a;
  }

  h3 {
    margin: 0 0 0.5rem;
  }
</style>
