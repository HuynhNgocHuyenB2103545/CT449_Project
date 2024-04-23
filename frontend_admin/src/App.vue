<script>
import AppHeader from "@/components/AppHeader.vue";
export default {
    components: {
        AppHeader,
    },
};
</script>

<template>
    <div id="app">
        <AppHeader />
        <div class="container mt-3">
            <router-view />
        </div>
    </div>
</template>

<style scoped>
#app {
  background-image: url("assets/bg1.jpg");
  background-size: 100% 100%;
  background-attachment: fixed;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
#body{
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

</style>