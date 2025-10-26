<script setup>

</script>

<template>
  <header>
  <h1 class="text-gradient">SMOLGRAM </h1>
  </header>
  <main>
    <slot />
  </main>
  <footer>
  <small>Created by Christian "Ace"</small>
    <a href="https://github.com/christiancode1296/FitnessApp" target="_blank">
      <img alt="pfp" src="https://avatars.githubusercontent.com/u/143355041?v=4"/>
      <p>Ace</p>
    </a>
  </footer>
</template>

<style scoped>
  header, footer, main {
    padding: 1rem;
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
  }


  main {
    flex: 1;
  }

  footer {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    align-items: center;
    padding: 2rem 0 3rem;

  }
  footer a {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.3rem 0.5rem 0.3rem 0.3rem;
    background: var(--background-muted);
    border-radius: 4rem;
    border: 1px solid transparent;
    transition-duration: 200ms;
    text-decoration: none;
  }
  footer a:hover {
    border-color: var(--color-link);
  }
  footer a img {
    max-width: 30px;
    aspect-ratio: 1/1;
    border-radius: 100%;
  }

</style>