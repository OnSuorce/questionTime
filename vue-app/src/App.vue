<template>
  <div id="nav"> <NavbarComponent></NavbarComponent> </div>
  <router-view/>
</template>

<script>
import NavbarComponent from "@/components/navbar.vue"
export default {
  name: "App",
  components:{
    NavbarComponent
  }
}
</script>
<style>
      html,
      body {
       
        font-family: "Noto Sans JP", sans-serif;
        font-weight: 400;
      }
</style>
