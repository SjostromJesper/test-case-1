<script setup>
defineProps({
  menuToggle: {
    type: Function,
    required: true
  },
  currentTab: {
    type: Number,
    required: true
  }
})
</script>

<template>
  <main>
    <header>
      <section class="logo-container">
        <img class="logo-image" alt="console logo" src="https://avatars3.githubusercontent.com/u/37439169?s=200&v=4"/>
        <h1>DEV APP</h1>
      </section>

      <nav class="navigation-container">
        <p class="navigation-link" :class="{active: currentTab === 0}" @click="() => menuToggle(0)">HOME</p>
        <p class="navigation-link" :class="{active: currentTab === 1}" @click="() => menuToggle(1)">CUSTOMERS</p>
      </nav>

      <section class="profile-container">
        <img class="profile-image"
             src="https://files.startdeliver.com/accid-aa909493a6679e232a361e2a501179b4/611d57c1d8af8f2671ed9c25fb38331b"
             alt="WUBWUBWUBWUWBUWB">

        <section class="profile-info">
          <p class="profile-name">John Zoidberg</p>
          <p class="profile-title">Customer Success Hero</p>
        </section>

      </section>
    </header>
    <slot/>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  width: 100%;
  padding-bottom: 3em;

  border-bottom: 1px solid #a4aabd;
}

header {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #a4aabd;
  padding-bottom: 4px;

  h1 {
    font-family: "Lato", sans-serif;
    color: #1c2c54;
  }
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 1rem;

  .logo-image {
    width: 40px;
    height: 40px;
  }
}

.navigation-container {
  display: flex;
  align-items: center;
  gap: 1rem;

  .navigation-link:hover {
    cursor: pointer;
  }

  .active {
    border-bottom: 2px solid #2050fe;
    color: #2050fe;
  }
}


.profile-container {
  display: flex;
  height: 30px;
  gap: 8px;

  .profile-image {
    width: auto;
    height: auto;

    border-radius: 100%;
  }

  .profile-info {
    .profile-title {
      color: #a4aabd;;
    }

    p {
      font-size: 0.8em;
    }

  }
}
</style>