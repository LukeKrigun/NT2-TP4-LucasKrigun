<template>

  <section class="src-components-formulario">
  <div class="jumbotron">
      <h2>Formulario</h2>
      <hr>
      <hr>
      <br>
      <vue-form :state="formState" @submit.prevent="enviar()">
    
        <!-- --------------------- -->
        <!--     Campo nombre      -->
        <!-- --------------------- -->
        <validate tag="div">
          <!-- Elemento de entrada -->
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

          <!-- Mensajes de validación -->
          <field-messages name="nombre" show="$dirty">
            <!-- <div class="alert alert-success mt-1">Success!</div> -->
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{nombreMinLength}} caracteres.
            </div>
            
            <div class="alert alert-danger mt-1" v-if="formData.nombre.length==nombreMaxLength">
              Alcanzaste el máximo de {{nombreMaxLength}} caracteres permitidos.
            </div>

            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>
          </field-messages>
        </validate>
        <br>

        <!-- --------------------- -->
        <!--      Campo edad       -->
        <!-- --------------------- -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="edad">Edad</label>
          <input 
            type="number"
            id="edad"
            name="edad" 
            class="form-control"
            autocomplete="off"
            v-model.number="formData.edad" 
            required 
            :min="edadMin"
            :max="edadMax"
          />

          <!-- Mensajes de validación -->
          <field-messages name="edad" show="$dirty">
            <!-- <div class="alert alert-success mt-1">Success!</div> -->
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad mínima permitida es de {{edadMin}} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad máxima permitida es de {{edadMax}} años.
            </div>
          </field-messages>
        </validate>
        <br>

        <!-- --------------------- -->
        <!--    Campo email     -->
        <!-- --------------------- -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="email">email</label>
          <input 
            type="email"
            id="email"
            name="email" 
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.email" 
            required 
          />

          <!-- Mensajes de validación -->
          <field-messages name="email" show="$dirty">
            <!-- <div class="alert alert-success mt-1">Success!</div> -->
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="email" class="alert alert-danger mt-1">Email no válido</div>
            
          </field-messages>
        </validate>
        <br>

        <!-- Botón de envío -->
        <button class="btn btn-success my-4" :disabled="formState.$invalid">Enviar</button>
<hr>
       <p><b>DATOS CARGADOS</b></p>
      <pre>Usuarios: {{ usuarios.length }}</pre>
      <pre>Nombre: {{ formData.nombre }}</pre>
      <pre>Edad: {{ formData.edad }}</pre>
      <pre>Email: {{ formData.email }}</pre>

      <div class="table-responsive">
              <table class="table table-dark" v-if="usuarios.length" >
                  <tr>
                      <th>ID</th>
                      <th>Nombre</th>
                      <th>Edad</th>
                      <th>Email</th>
                  </tr>
                  <tr v-for="(usuarios,index) in usuarios" :key="index">
                      <td>{{ index + 1 }}</td>
                      <td>{{ usuarios.nombre }}</td>
                      <td>{{ usuarios.edad }}</td>
                      <td>{{ usuarios.email }}</td>
                  </tr>
              </table>
              <div class="alert alert-danger mt-1" v-else>
                <p>No hay datos cargados</p>
              </div>
      </div>


      </vue-form>
  </div>

  
  </section>

</template>

<script>

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState:{},
        formData:this.getInicialData(),
        nombreMinLength:5,
        nombreMaxLength:15,
        edadMin:18,
        edadMax:120,
        usuarios:[]
      }
    },
    methods: {
      getInicialData() {
        return {
          nombre: '',
          edad: '',
          email: ''
        }
      },

agregar(){
        const usuario={
          nombre:this.formData.nombre,
          edad:this.formData.edad,
          email:this.formData.email
        }
        this.usuarios.push(usuario);

        //GUARDA USUARIOS EN LOCAL STORAGE
        localStorage.setItem("usuarios", JSON.stringify(this.usuarios));
      },

    created(){
      let data = localStorage.getItem("usuarios");
      if(data != null){
        this.usuarios = JSON.parse(data);
        console.log("Usuario guardado en localStorage!");
      } 

    },
      enviar() {
        this.agregar()
        console.log({ ...this.formData })

        this.formData = this.getInicialData() 
        this.formState._reset()  
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">


  .jumbotron {
     /* Permalink - use to edit and share this gradient: https://colorzilla.com/gradient-editor/#808080+20,9d9d9d+50,808080+80&0+0,0.8+15,1+19,1+81,0.8+85,0+100 */
background: -moz-linear-gradient(-45deg,  rgba(128,128,128,0) 0%, rgba(128,128,128,0.8) 15%, rgba(128,128,128,1) 19%, rgba(128,128,128,1) 20%, rgba(157,157,157,1) 50%, rgba(128,128,128,1) 80%, rgba(128,128,128,1) 81%, rgba(128,128,128,0.8) 85%, rgba(128,128,128,0) 100%); /* FF3.6-15 */
background: -webkit-linear-gradient(-45deg,  rgba(128,128,128,0) 0%,rgba(128,128,128,0.8) 15%,rgba(128,128,128,1) 19%,rgba(128,128,128,1) 20%,rgba(157,157,157,1) 50%,rgba(128,128,128,1) 80%,rgba(128,128,128,1) 81%,rgba(128,128,128,0.8) 85%,rgba(128,128,128,0) 100%); /* Chrome10-25,Safari5.1-6 */
background: linear-gradient(135deg,  rgba(128,128,128,0) 0%,rgba(128,128,128,0.8) 15%,rgba(128,128,128,1) 19%,rgba(128,128,128,1) 20%,rgba(157,157,157,1) 50%,rgba(128,128,128,1) 80%,rgba(128,128,128,1) 81%,rgba(128,128,128,0.8) 85%,rgba(128,128,128,0) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#00808080', endColorstr='#00808080',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */

      color: white;
  }

  hr {
      background-color: #bbb;
  }  

  pre {
    color: white;
  }
  
</style>
