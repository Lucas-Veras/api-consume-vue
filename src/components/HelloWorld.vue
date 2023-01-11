<script lang="ts">
import { onMounted, ref } from 'vue';
/* Forma antiga sem setup */
export default {
  name: "HelloWorld",
  props: {
    msg: String, 
    bool: Boolean
  },
  methods: {
    increment() {
      this.data++
    }
  },
  data() {
    return {
      data: 1
    }
  },
  created(){
    console.log(this.bool, "teste1")
    console.log("render created 1")
  },
  mounted() {
    console.log(this.bool, "teste2")
    console.log("render mounted 2")
  }
}


/* forma nova sem setup */
/*
export default {
  props: {
    msg: String, 
    bool: Boolean
  },
  setup({msg, bool}) {
    console.log(msg)
    console.log(bool)
    const data = 1
    onMounted(() => {
      console.log("render 2")
    })
    console.log("render 1")

    return {data}
  },
}
*/


  /* forma nova PRECISA DO SETUP NA TAG SCRIPT */
/*
  const {msg, bool} = defineProps({
    msg: String,
    bool: Boolean
  })

  const data = 1
*/
</script>

<template>
  <h1>{{ msg }} {{ bool }} {{ data }}</h1>
</template>

<style scoped>
</style>

