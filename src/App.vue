<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-primary">
      <a href="/" class="navbar-brand">Inicio</a>
    </nav>
    <div class="container">
      <div class="row mt-5">
        <div class="col-sm-4">
          <div class="card">
            <div class="card-header">
              <h3>Agrega algo nuevo</h3>
            </div>
            <div class="card-body">
              <form @submit="addNewObject">
                <div class="form-group">
                  <input type="text" class="form-control" v-model="newObject.name" placeholder="Ingrese el nombre">
                </div>
                 <div class="form-group">
                  <input type="number" class="form-control" v-model="newObject.age" placeholder="Ingrese el edad">
                </div>
                 <div class="form-group">
                  <input type="text" class="form-control" v-model="newObject.description" placeholder="Ingrese una descripcion">
                </div>
                <button type="submit" class="btn btn-primary "  > Guardar </button>
              </form>
            </div>
          </div>
        </div>
        <div class="col-sm-8">
          <div class="card">
            <div class="card-header">
              <h3>Lista de objetos</h3>
            </div>
            <div class="card-body">
              <table class="table table-striped table-bordered">
                <thead>
                  <tr>
                    <th scope="col">#</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Edad</th>
                    <th scope="col">Descripcion</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="usuario in usuarios" :key="usuario.login.uuid" >
                     <td>{{ usuario.gender }}</td>
                      <td>{{ usuario.name.first }}</td>
                     <td>{{ usuario.name.last }}</td>
                    <td>{{ usuario.name.title }}</td>


                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

async function savePerson(person){
  let {data} = await axios.post('http://localhost:5000/api/Person', person );

  alert(data);
}
export default {
  name: "app",
  components: {},
  data(){
    return {
      newObject: {
        name: '',
        age: '',
        description: ''
      },
      usuarios:[]
    };
  },
  mounted(){
    this.leerApi()
  },
  methods: {
    async addNewObject() {
      await savePerson(this.newObject);

    },
    async leerApi(){
      try{
          let {data} = await  axios.get('https://localhost:5001/api/Person');
          console.log(data);
          this.usuarios = data;
      }catch(err){
        alert(err);
      }

    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
