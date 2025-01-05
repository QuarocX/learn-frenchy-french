<div class="account-view">
  <h1>My Account</h1>
  <div class="profile-info">
    <div class="avatar">👤</div>
    <h2>Demo User</h2>
    <p>Learning French since January 2024</p>
    <div class="stats">
      <div class="stat">
        <h3>5</h3>
        <p>Days Streak</p>
      </div>
      <div class="stat">
        <h3>25</h3>
        <p>Words Learned</p>
      </div>
    </div>
  </div>
</div>

<style>
  .account-view {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
    text-align: center;
  }

  .profile-info {
    margin-top: 2rem;
  }

  .avatar {
    font-size: 4rem;
    margin-bottom: 1rem;
  }

  .stats {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-top: 2rem;
  }

  .stat {
    padding: 1rem;
    background: #f5f5f5;
    border-radius: 8px;
    min-width: 120px;
  }

  .stat h3 {
    margin: 0;
    font-size: 1.5rem;
    color: #4a90e2;
  }

  .stat p {
    margin: 0.5rem 0 0;
    font-size: 0.9rem;
  }

  :global(body.dark-mode) .stat {
    background: #2a2a2a;
  }
</style>
