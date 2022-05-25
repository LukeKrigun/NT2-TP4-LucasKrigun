<template >



  <section class="src-components-usuarios">

     <!-- XMLHttpRequest y fetch -->
     <div class="jumbotron">
      <h2>Componente usuarios -  XMLHttpRequest, fetch y Axios</h2>
      <hr>
      <hr>
      <br>

      <button class="btn btn-warning my-3 mr-3" @click="getUsuariosXHRcb()">Pedir XHR (cb)</button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosXHRpromise()">Pedir XHR (promise)</button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosFetch()">Pedir Fetch </button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Pedir Axios </button>
      <button class="btn btn-danger my-3" @click="usuarios=[]">CLEAR</button>
      <br>

        <div v-if="usuarios.length" class="table-responsive">
       <div class="table">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Telefono</th>
          </tr>
          <tr v-for="(usuario, index) in usuarios" :key="index">
              <td>{{ usuario.nombre }}</td>
              <td>{{ usuario.email }}</td>
              <td>{{ usuario.telefono }}</td>
          </tr>
        </table>
        <h5 class="alert alert-primary">Se encontraron {{usuarios.length}} usuarios.</h5>
        </div>
      </div>
      <h4 v-else class="alert alert-danger text-center">No se encontraron usuarios</h4>

     </div>
  

  </section>



</template>

<script >

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {

        this.getUsuarios()

    },
    data () {
      return {
        url: 'https://62899c135da6ddfd5d59ddef.mockapi.io/usuarios',
        usuarios: []
      }
    },
    methods: {
        /* XMLHttpRequest y fetch */
      wrapperXHRpromise() {
        return new Promise((resolve,reject) => {
         
          const xhr = new XMLHttpRequest()
          xhr.open('get', this.url)

          xhr.addEventListener('load', () => {
            if(xhr.status == 200) {
              let respuesta = JSON.parse(xhr.response)
              //console.log(respuesta)
              resolve(respuesta)
            }
            else {
              console.error('ERROR XHR cb (status)', xhr.status)
              let error = {
                title: 'ERROR XHR cb (status)',
                status: xhr.status
              }
              reject(error)
            }
          })

          xhr.addEventListener('error', e => {
              console.error('ERROR XHR cb (ajax)', e)
              let error = {
                title: 'ERROR XHR cb (ajax)',
                info: e
              }
              reject(error)
          })

          xhr.send()
        })
      },
      /* -------------------------------------------------------------------- */
      /*   Petición Ajax (Asynchronous Javascript And XML) con XHR callback   */
      /* -------------------------------------------------------------------- */
      getUsuariosXHRcb() {
          const xhr = new XMLHttpRequest()
          xhr.open('get', this.url)

          xhr.addEventListener('load', () => {
            if(xhr.status == 200) {
              let respuesta = JSON.parse(xhr.response)
              //console.log(respuesta)
              this.usuarios = respuesta
            }
            else {
              console.error('ERROR XHR cb (status)', xhr.status)
            }
          })

          xhr.addEventListener('error', e => {
              console.error('ERROR XHR cb (ajax)', e)
          })

          xhr.send()
      },
      /* -------------------------------------------------------------------------------------------- */
      /*   Petición Ajax (Asynchronous Javascript And XML) con XHR callback wrapeado en una promise   */
      /* -------------------------------------------------------------------------------------------- */
      async getUsuariosXHRpromise() {
        
          // -----  UTILIZANDO LA SINTAXIS ASYNC/AWAIT ----
          try {
            let respuesta = await this.wrapperXHRpromise()
            //console.log(respuesta)
            this.usuarios = respuesta
          }
          catch(error) {
            console.error('Error XHRpromise', error)
          }
      },
      /* ------------------------------------------------------------- */
      /*   Petición Ajax (Asynchronous Javascript And XML) con Fetch   */
      /* ------------------------------------------------------------- */
      async getUsuariosFetch() {
      
        // -----  UTILIZANDO LA SINTAXIS ASYNC/AWAIT ----
        try {
          let response = await fetch(this.url)
          //console.log(response)
          let respuesta = await response.json()
          this.usuarios = respuesta
        }
        catch(error) {
          console.error('Error Fetch', error)
        }
      },
        /* AXIOS */
       async getUsuariosAxios() {              
        try {
          let { data } = await this.axios(this.url)
          this.usuarios = data
        }
        catch(error) {
          console.error('Error Axios', error)
        }   
      },
      deleteUsuarios(){
        this.usuarios=[]
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
 

    .jumbotron {
/* Permalink - use to edit and share this gradient: https://colorzilla.com/gradient-editor/#000000+0,000000+100&0.65+0,0+100;Neutral+Density */
background: -moz-linear-gradient(-45deg,  rgba(0,0,0,0.65) 0%, rgba(0,0,0,0) 100%); /* FF3.6-15 */
background: -webkit-linear-gradient(-45deg,  rgba(0,0,0,0.65) 0%,rgba(0,0,0,0) 100%); /* Chrome10-25,Safari5.1-6 */
background: linear-gradient(135deg,  rgba(0,0,0,0.65) 0%,rgba(0,0,0,0) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#a6000000', endColorstr='#00000000',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */


     text-align: center;

  }

  .table {
   /* Permalink - use to edit and share this gradient: https://colorzilla.com/gradient-editor/#1e5799+0,7db9e8+100&1+0,0+100;Blue+to+Transparent */
background: -moz-linear-gradient(45deg,  rgba(30,87,153,1) 0%, rgba(125,185,232,0) 100%); /* FF3.6-15 */
background: -webkit-linear-gradient(45deg,  rgba(30,87,153,1) 0%,rgba(125,185,232,0) 100%); /* Chrome10-25,Safari5.1-6 */
background: linear-gradient(45deg,  rgba(30,87,153,1) 0%,rgba(125,185,232,0) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#1e5799', endColorstr='#007db9e8',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */

  }

</style>
