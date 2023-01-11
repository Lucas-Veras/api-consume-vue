<template>
<!--<HelloWorld msg="teste" :bool="true" />-->
  <router-view/>
</template>

<script lang="ts">
import HelloWorld from './components/HelloWorld.vue';
import "./App.css"

export default {
    name: "app",
    components: { HelloWorld }
}
</script>
