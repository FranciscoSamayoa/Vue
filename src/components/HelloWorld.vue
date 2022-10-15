<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>Proyecto Final</h1>
    <br>
    <h1>Francisco Samayoa Carmona</h1>
    <br>
    <!--
       <h1 v-if="author.name == 'Oscar'">Eso es correcto</h1>
      <h1 v-else>Esta mal el author</h1>
      <br>
      <br>
    -->
  
  <table class="table thead-dark">
  <thead>
    <tr>
      <th scope="col">id</th>
      <th scope="col">Titulo</th>
      <th scope="col">Body</th>
      <th scope="col">Acciones</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="posts in listaPosts" :key="posts.id">
      <td>{{ posts.id }}</td>
      <td>{{ posts.title }}</td>
      <td>{{ posts.body }}</td>
      <td> 
        <b-button :to="'/detalle/' + posts.id" class="btn btn-info"> Ver mas </b-button>
      </td>
    </tr>
  </tbody>
</table>


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    id: Number,
  },
  data(){
    return {
      author: {
        name: 'Jhon Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      },
      carros: {
        name: null,
        colores: []
      },
      listaPosts: [],
    }
  },

  created(){
    this.obtenerApi();
  },

  methods:{
    obtenerApi(){
      let apiURL = 'https://jsonplaceholder.typicode.com/posts';
      this.listaPosts= [];

      this.$http.get(apiURL).then(response => {
        if(response.status == 200){
        let data = response.data;

        data.forEach((element, index) =>{
          if (index + 1  <= 30){
            this.listaPosts.push(element)
          }
        });
        }
      })
      .catch(e => console.log(e))
      .finally(()=>console.log("Error"))
    }
  },
}
</script>
