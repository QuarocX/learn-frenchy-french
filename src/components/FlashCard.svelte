<script>
  const flashcards = [
    {
      french: "Le petit déjeuner",
      english: "Breakfast",
      example: "Je prends mon petit déjeuner à 8h.",
    },
    {
      french: "Le déjeuner",
      english: "Lunch",
      example: "C'est l'heure du déjeuner!",
    },
    {
      french: "Le dîner",
      english: "Dinner",
      example: "Nous préparons le dîner ensemble.",
    },
    {
      french: "La cuisine",
      english: "Kitchen",
      example: "La cuisine est moderne.",
    },
    {
      french: "Le restaurant",
      english: "Restaurant",
      example: "Allons au restaurant!",
    },
  ];

  let currentCardIndex = 0;
  let isFlipped = false;

  const flipCard = () => {
    isFlipped = !isFlipped;
  };

  const nextCard = () => {
    currentCardIndex = (currentCardIndex + 1) % flashcards.length;
    isFlipped = false;
  };

  const previousCard = () => {
    currentCardIndex =
      (currentCardIndex - 1 + flashcards.length) % flashcards.length;
    isFlipped = false;
  };
</script>

<div class="activity-view">
  <header>
    <h1>Daily French Vocabulary</h1>
    <p class="theme">Today's Theme: Food & Dining</p>
  </header>

  <div class="instructions">
    <h2>How to Practice:</h2>
    <ol>
      <li>Click the card to see the translation</li>
      <li>Say the word out loud in French</li>
      <li>Try using it in the example sentence</li>
      <li>Move to the next card when ready</li>
    </ol>
  </div>

  <div class="flashcard-container">
    <div class="progress-and-controls">
      <div class="progress">
        Card {currentCardIndex + 1} of {flashcards.length}
      </div>
      <div class="controls">
        <button class="nav-button prev" on:click={previousCard}>←</button>
        <button class="nav-button next" on:click={nextCard}>→</button>
      </div>
    </div>

    <div class="flashcard {isFlipped ? 'flipped' : ''}" on:click={flipCard}>
      <div class="card-front">
        <h3>{flashcards[currentCardIndex].french}</h3>
        <p class="example">{flashcards[currentCardIndex].example}</p>
      </div>
      <div class="card-back">
        <h3>{flashcards[currentCardIndex].english}</h3>
        <p class="tip">Practice saying the French version!</p>
      </div>
    </div>
  </div>
</div>

<style>
  .activity-view {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem 2rem 5rem 2rem;
  }

  header {
    text-align: center;
    margin-bottom: 2rem;
  }

  .theme {
    color: #4a90e2;
    font-size: 1.2rem;
  }

  .instructions {
    background: #f5f5f5;
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
  }

  :global(body.dark-mode) .instructions {
    background: #2a2a2a;
  }

  .flashcard-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    margin: 2rem 0;
  }

  .progress-and-controls {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    max-width: 500px;
    margin-bottom: 1rem;
  }

  .controls {
    display: flex;
    gap: 1rem;
  }

  .nav-button {
    padding: 0.8rem;
    border: none;
    border-radius: 50%;
    background: #4a90e2;
    color: white;
    cursor: pointer;
    transition: all 0.3s;
    font-size: 1.2rem;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .nav-button:hover {
    background: #357abd;
    transform: scale(1.1);
  }

  :global(body.dark-mode) .nav-button {
    background: #2a2a2a;
  }

  :global(body.dark-mode) .nav-button:hover {
    background: #444;
  }

  .flashcard {
    width: 100%;
    max-width: 500px;
    height: 300px;
    perspective: 1000px;
    cursor: pointer;
    transform-style: preserve-3d;
    transition: transform 0.6s;
  }

  .flashcard.flipped {
    transform: rotateY(180deg);
  }

  .card-front,
  .card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 12px;
    padding: 2rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .card-front {
    background: white;
    border: 2px solid #e0e0e0;
  }

  .card-back {
    background: #4a90e2;
    color: white;
    transform: rotateY(180deg);
  }

  :global(body.dark-mode) .card-front {
    background: #2a2a2a;
    border-color: #444;
  }

  :global(body.dark-mode) .card-back {
    background: #1a1a1a;
  }

  h3 {
    font-size: 2rem;
    margin: 0 0 1rem;
  }

  .example {
    font-style: italic;
    color: #666;
    margin-top: 1rem;
  }

  .tip {
    font-size: 1.1rem;
    margin-top: 1rem;
  }

  @media (max-width: 600px) {
    .activity-view {
      padding: 1rem;
      padding-bottom: 5rem;
    }

    .progress-and-controls {
      padding: 0 1rem;
    }

    .nav-button {
      width: 35px;
      height: 35px;
      font-size: 1rem;
      padding: 0.5rem;
    }
  }
</style>
