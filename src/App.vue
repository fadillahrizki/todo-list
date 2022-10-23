<template>
  <header>
    <Navbar data-cy="header-background" />
  </header>

  <RouterView />
</template>

<script>
import Navbar from './components/Navbar.vue';
export default {
    components: { Navbar }
}
</script>
