<template>
  <main class="app">
    <NavigationTop />
    <router-view id="router"></router-view>
    <Offline />
    <NavigationBottom />
  </main>
</template>

<script>
import NavigationTop from './components/NavigationTop.vue';
import NavigationBottom from './components/NavigationBottom.vue';
import Offline from './components/Offline.vue';

import mongoosy from 'mongoosy/frontend';
const { Upload } = mongoosy;

export default {
  components: {
    NavigationTop,
    NavigationBottom,
    Offline,
  },
  async created() {
    this.$store.dispatch('check');
  },
  async mounted() {
    const count = await Upload.countDocuments();
    this.$store.commit('setUploadCount', count);
    this.$store.commit('resetUploadOffset');
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  scroll-behavior: smooth;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#router {
  max-height: 100%;
  margin: 0;
  padding: 1rem;
  overflow: auto;
}
main.app {
  display: grid;
  grid-template-rows: min-content auto min-content;
  height: 100vh;
}
.input-field input {
  line-height: 0 !important;
}
.input-field input[type='text']:focus,
.input-field input[type='email']:focus,
.input-field input[type='password']:focus {
  border-bottom: 1px solid #00acc1 !important;
  box-shadow: 0 1px 0 0 #00acc1 !important;
}
.input-field input[type='text']:focus + label,
.input-field input[type='email']:focus + label,
.input-field input[type='password']:focus + label {
  color: #00acc1 !important;
}
div.chip {
  display: inline-flex;
  max-width: 50vw;
  white-space: nowrap;
  text-overflow: ellipsis;
}
div.chip span {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
div.chip i {
  flex: 1;
}
</style>
