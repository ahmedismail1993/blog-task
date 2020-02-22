<template>
  <div id="app">
    <div id="nav">
      <Navbar />
    </div>
    <router-view />
  </div>
</template>
<script>
export default {
  name: "App",
  components: {
    Navbar: () => import("@/components/navbar")
  }
};
</script>
