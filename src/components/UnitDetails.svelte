<script>
  export let unit;
  export let onClose;
</script>

<div class="overlay" on:click={onClose}>
  <div class="modal" on:click|stopPropagation>
    <button class="close-button" on:click={onClose}>×</button>
    <h2>{unit.name}</h2>
    <p>{unit.description}</p>
    <!-- Add more unit details here -->
  </div>
</div>

<style>
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .modal {
    background: white;
    padding: 2rem;
    border-radius: 8px;
    max-width: 500px;
    width: 90%;
    position: relative;
  }

  :global(body.dark-mode) .modal {
    background: #2a2a2a;
    color: white;
  }

  .close-button {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    padding: 0.5rem;
  }

  :global(body.dark-mode) .close-button {
    color: white;
  }
</style>
