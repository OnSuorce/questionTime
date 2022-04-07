<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
        <router-link class="navbar-brand"  :to="{name: 'home'}">QuestionTime</router-link>
      
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto"><a class="btn btn-outline-secondary" href="/accounts/logout/">Logout</a></ul>
          
        
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavbarComponent",
};
</script>

<style>
.navbar-brand{
    font-weight: bold;
    font-size: 1505;
}
.navbar-brand:hover{
    color: red
}
.navbar{
    border-bottom: 1px solid #ddd;
}
</style>