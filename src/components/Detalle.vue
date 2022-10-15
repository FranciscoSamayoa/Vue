<template>
    <div>
        <h1>Detalle</h1>
      <br>
      <label>Editar: </label>
      <input v-model="objeto.title" placeholder="editeme" class="col-lg-6">
      <br>
      <table class="table thead-dark ">
        <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Titulo</th>
          <th scope="col">Body</th>

        </tr>
        </thead>
        <tbody>
        <tr>
          <td>{{ objeto?.id }}</td>
          <td>{{ objeto?.title }}</td>
          <td>{{ objeto?.body }}</td>

        </tr>
        </tbody>
      </table>
      <br>
      <br>
      <b-button to="/" class="btn btn-info"> Inicio </b-button>
    </div>
</template>

<script>
export default {
    name: 'detalle-info',
    props: {
        id: Number
    },
  data(){
      return{
        idObjeto: Number,
        objeto: null
      }
  },
  created() {
      this.idObjeto = this.$route.params.id;
      this.obtenerDetalle();
  },
  methods:{
      obtenerDetalle(){
        this.$http.get("https://jsonplaceholder.typicode.com/posts/" + this.idObjeto)
            .then((response)=>{
              this.objeto = response.data;

              console.log(response);
            })
      }
  }

}
</script>