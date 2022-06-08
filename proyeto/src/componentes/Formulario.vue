<template>

  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2><i>Notas alumnos</i></h2>
      <hr>
      <hr>
      <br>

      <vue-form :state="formState" @submit.prevent="enviar()">
    
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text"
            id="nombre"
            name="nombre" 
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.nombre" 
            required 
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          />

          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
           
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{nombreMinLength}} caracteres.
            </div>
          
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>
          </field-messages>
        </validate>
        <br>

        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input 
            type="text"
            id="apellido"
            name="apellido" 
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.apellido" 
            required 
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          />

          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>

            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{nombreMinLength}} caracteres.
            </div>

             <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>

          </field-messages>
        </validate>
        <br>

        
        <validate tag="div">
          <label for="nota">Nota</label>
          <input 
            type="number"
            id="nota"
            name="nota" 
            class="form-control"
            autocomplete="off"
            v-model.number="formData.nota" 
            required 
            :min="notaMin"
            :max="notaMax"
          />

          
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">
              La nota mínima es de {{notaMin}}
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La nota máxima es de {{notaMax}}
            </div>
          </field-messages>
        </validate>
        <br>


        <button class="btn btn-success my-4" :disabled="formState.$invalid">Enviar</button>
      </vue-form>      

    <h2><i>Detalle de Notas</i></h2>
      <br>

      <div v-if="notas.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Alumno</th>
            <th>Nota</th>
          </tr>
          <tr v-for="(n,index) in notas" :key="index" >
            <td>{{ n.nombre  + " " + n.apellido }}</td>
            <td :style="{color: color(n)}">{{n.nota}} </td>
            
          </tr>
          <th scope="row">PROMEDIO TOTAL:</th>
          <td :style="{
            color: analizarNota(calcularPromedio),
          }"> {{calcularPromedio}} </td>
        </table>
      </div>
      <h3 v-else class="alert alert-info">No hay notas ingresadas</h3>

    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-formulario-av',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState : {},
        formData : this.getInicialData(),
        notas : [],
        nombreMinLength : 3,
        nombreMaxLength : 15,
        notaMin: 0,
        notaMax: 10
      }
    },
    methods: {
      getInicialData() {
        return {
          nombre: '',
          apellido: '',
          nota: '',
        }
      },
      
      enviar() {
        let nota = { ...this.formData }
        console.log(nota)
        this.notas.push(nota)
        this.totalNotas = this.totalNotas + Number(this.formData.nota); 
      
        this.formData = this.getInicialData() 
        this.formState._reset()  
      },
      analizarNota(nota) {
        var color;
        if(nota<4) {
          color = "red";
        } else if (nota>=4 && nota<7){
          color = "yellow";
        }else{
          color = "green";
        }
        
        return color;
      },
      color(n){
        var numero= n.nota;
        return this.analizarNota(numero);
      }
      
    },
    computed: {
      calcularPromedio(){
        let promedio =this.notas.length
        if(this.notas.length>0){
        promedio = Number(this.totalNotas/this.notas.lenght)}
        return  promedio
        
      }
    }
}


</script>

<style scoped lang="css">
  .src-componentes-formulario-av {

  }

  .jumbotron {
      background-color: rgb(139, 173, 173);
      color: white;
  }

  hr {
      background-color: #bbb;
      color: rgb(0, 128, 0)
  }  

</style>
