<template>
   <div id="app">
      <WhereToEat msg="รับประทานข้าวที่ไหนดี " />
   </div>
</template>

<script>
import WhereToEat from "./components/WhereToEat.vue";

export default {
   name: "App",
   components: {
      WhereToEat,
   },
};
</script>

<style>
#app {
   font-family: "Itim", cursive;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   /* text-align: center; */
   color: #2c3e50;
   height: 100vh;
   padding: 18px;
   margin-left: auto;
   margin-right: auto;
   width: 100vw;
   max-width: 600px;
   /* background-color: #bdd5ea; */
   /* display: flex;
   justify-content: center;
   align-items: center; */
}
</style>
