<template>
  <div class="home">
    <img alt="surway logo" src="../assets/logo.png">
    <HelloWorld msg="do it the surway"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'Home',
  components: {
    HelloWorld,
  },
};
</script>
