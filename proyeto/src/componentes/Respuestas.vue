<template>

  <section class="src-componentes-choice">
    <div class="jumbotron">
      <h2><i> Respuestas Choice</i></h2>

<table class="table table-striped">
  <thead>
    <tr>
      <th scope="col">Número de Pregunta</th>
      <th scope="col">Respuesta</th>
    
    </tr>
  </thead>
  <tbody>
    <tr>

      <tr v-for="(pregunta,index) in preguntas" :key="index">
      <td>{{pregunta.numero }}</td>
      <td>{{pregunta.respuestas}}</td>
      </tr>
      
  </tbody>
</table>

      <hr>
      <br>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-choice',
    props: [],
    mounted () {

    },
    data () {
      return {
          preguntas: [
          { numero: 1, respuestas: ['c'] },
          { numero: 2, respuestas: ['c'] },
          { numero: 3, respuestas: ['a', 'b'] }
        ],

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron {
background-color: rgba(100, 105, 66, 0.396);
color: rgb(71, 33, 33);
  }
</style>
