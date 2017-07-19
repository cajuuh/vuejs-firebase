 <template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Vue.js 2 & Firebase Simple Application</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Adicionar Livro</h3>
      </div>
      <div class="panel-body">
        <form id="form" class="form-inline" v-on:submit.prevent="adicionaLivro">
          <div class="form-group">
            <label for="títuloLivro">Título:</label>
            <input type="text" id="títuloLivro" class="form-control" v-model="novoLivro.título"/>
          </div>
          <div class="form-group">
            <label for="autorLivro">Autor:</label>
            <input type="text" id="autroLivro" class="form-control" v-model="novoLivro.autor"/>
          </div>
          <div class="form-group">
            <label for="urlLivro">URL:</label>
            <input type="text" id="urlLivro" class="form-control" v-model="novoLivro.url"/>
          </div>
          <input type="submit" class="btn btn-primary" value="Adiciona Livro" />
        </form>
      </div>
    </div>
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Lista de Livros</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Título
              </th>
              <th>
                Autor
              </th>
              <th>
                Apagar
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="livro in livros">
              <td>
                <a v-bind:href="livro.url">{{livro.título}}</a>
              </td>
              <td>
                {{livro.autor}}
              </td>
              <td>
                <span class="glyphicon glyphicon-trash" v-on:click="removeLivro(livro)"></span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <!-- <router-view></router-view> -->
  </div>
</template>

<script>

import Firebase from 'firebase'

let config = {
  apiKey: "AIzaSyBVl1py249gg-QzYzH7R_DVUnH2SZcYzis",
  authDomain: "vuejs-firebase-test-5e3ba.firebaseapp.com",
  databaseURL: "https://vuejs-firebase-test-5e3ba.firebaseio.com",
  projectId: "vuejs-firebase-test-5e3ba",
  storageBucket: "vuejs-firebase-test-5e3ba.appspot.com",
  messagingSenderId: "623969585273"
}

let app = Firebase.initializeApp(config)
let db = app.database();

let livrosRef = db.ref('livros');

export default {
  name: 'app',
  firebase:{
    livros: livrosRef
  },
  data (){
    return{
      novoLivro:{
        título: '',
        autor: '',
        url:''
      }
    }
  },
  methods:{
      adicionaLivro: function(){
      livrosRef.push(this.novoLivro);
      this.novoLivro.título = '';
      this.novoLivro.autor = '';
      this.novoLivro.url = '';
    },
      removeLivro: function(livro){
        livrosRef.child(livro['.key']).remove();
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
