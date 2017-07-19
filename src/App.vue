 <template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Vue.js 2 & Firebase Simple Application</h1>
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
      novoLivro{
        título: '',
        autor: '',
        url:''
      }
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
