<template>
 
<div class="container-fluid mt-3">
   <div class="jumbotron">
     <h1> Parcial - PAYO PILAR</h1>
     <hr>
     <NavBar/>
  
     <router-view></router-view>


   </div>
 </div>

</template>

<script>
import NavBar from './componentes/NavBar.vue'



export default {
  name: 'App',
  components: {
  
    NavBar,
    
  }
}
</script>

<style>
 h1{
   color:rgb(83, 55, 75);
 }
 

</style>

