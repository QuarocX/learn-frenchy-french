<script>
  import { onMount } from "svelte";
  import ActivityCard from "./components/ActivityCard.svelte";
  import UnitDetails from "./components/UnitDetails.svelte";
  import FlashCard from "./components/FlashCard.svelte";
  import AccountView from "./components/AccountView.svelte";
  import NavigationBar from "./components/NavigationBar.svelte";
  import ViewTransition from "./components/ViewTransition.svelte";

  let units = [];
  let error = null;
  let darkMode = false;
  let selectedUnit = null;
  let currentView = "start";

  const handleUnitClick = (unit) => {
    selectedUnit = unit;
  };

  const closeUnitDetails = () => {
    selectedUnit = null;
  };

  const openFlashcards = () => {
    currentView = "activity";
  };

  const handleNavigation = (view) => {
    currentView = view;
    if (view === "start") {
      selectedUnit = null;
    }
  };

  onMount(async () => {
    try {
      console.log("Fetching data...");
      // import.meta.env.PROD is a Vite environment variable that is:
      // - false during development (npm run dev)
      // - true during production (npm run build)
      const API_URL = `${import.meta.env.VITE_API_URL}/french-class`;
      // const API_URL = "http://localhost:3000/french-class";
      console.log("API_URL:", API_URL);
      const response = await fetch(API_URL);
      console.log("Response:", response);

      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      const data = await response.json();
      units = data.quickActivities;
      console.log("Received units:", units);
    } catch (error) {
      console.error("Error loading activities:", error);
      error = error.message;
      units = [];
    }
  });

  $: if (typeof document !== "undefined") {
    document.body.classList.toggle("dark-mode", darkMode);
  }
</script>

{#if currentView === "start"}
  <ViewTransition key="start">
    <main>
      <div class="header">
        <h1>Learn Frenchy</h1>
        <button class="theme-toggle" on:click={() => (darkMode = !darkMode)}>
          {darkMode ? "☀️" : "🌙"}
        </button>
      </div>

      <section class="quick-access">
        <h2>Quick Access</h2>
        <div class="quick-links">
          <button class="flashcard-link" on:click={openFlashcards}>
            📝 Practice Flashcards
          </button>
        </div>
      </section>

      <section>
        <h2>French Units</h2>
        <ul>
          {#if error}
            <li class="error">Error: {error}</li>
          {:else if units.length > 0}
            {#each units as unit}
              <ActivityCard {unit} onClick={handleUnitClick} />
            {/each}
          {:else}
            <li>Loading activities...</li>
          {/if}
        </ul>
      </section>
    </main>

    {#if selectedUnit}
      <UnitDetails unit={selectedUnit} onClose={closeUnitDetails} />
    {/if}
  </ViewTransition>
{:else if currentView === "activity"}
  <ViewTransition key="activity">
    <FlashCard />
  </ViewTransition>
{:else if currentView === "account"}
  <ViewTransition key="account">
    <AccountView />
  </ViewTransition>
{/if}

<NavigationBar {currentView} onNavigate={handleNavigation} />

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    transition:
      background-color 0.3s,
      color 0.3s;
  }

  :global(body.dark-mode) {
    background-color: #1a1a1a;
    color: #ffffff;
  }

  main {
    font-family: Arial, sans-serif;
    max-width: 600px;
    margin: 2rem auto;
    text-align: left;
    padding: 1rem;
    transition:
      background-color 0.3s,
      color 0.3s;
    margin-bottom: 4rem;
  }

  .quick-access {
    margin: 2rem 0;
    text-align: center;
  }

  .quick-links {
    display: flex;
    justify-content: center;
    gap: 1rem;
  }

  .flashcard-link {
    padding: 1rem 2rem;
    font-size: 1.1rem;
    background-color: #4a90e2;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition:
      transform 0.2s,
      background-color 0.3s;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .flashcard-link:hover {
    transform: translateY(-2px);
    background-color: #357abd;
  }

  :global(body.dark-mode) .flashcard-link {
    background-color: #2a2a2a;
  }

  :global(body.dark-mode) .flashcard-link:hover {
    background-color: #444;
  }

  h1 {
    text-align: center;
  }

  section {
    margin-top: 2rem;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  .theme-toggle {
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    padding: 0.5rem;
    border-radius: 50%;
  }

  .theme-toggle:hover {
    background-color: #eee;
  }

  :global(body.dark-mode) .theme-toggle:hover {
    background-color: #333;
  }
</style>
