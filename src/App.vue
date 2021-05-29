<template>
  <div id="app">

      <h1>Bem Vindo À Consulta de CEP</h1>
          <input type="text" v-model="cep" class="pesquisa" placeholder="ex: 45611-800
">
          <button @click="pegaCep()" class="button">{{msg}}</button>
                          <hr/> 
            <div v-if="status" class="form">
              <input type="text" :value="response['bairro']">
              <input type="text" :value="response['logradouro']">
              <input type="text" :value="response['localidade']">
              <input type="text" :value="response['ddd']">

            </div>
    
    
  </div>
</template>

<script>
const axios = require('axios')

export default {
  //itens que são reativos.
  name: 'App',
  data(){
    return {
      msg: 'Verificar CEP',
      cep: '',
      response: [],
      status: false
    }
  },
  //Axios para chamar a api
  methods:{ 
   pegaCep:  async function(){
          var cep = this.cep.replace('-', '')
        if (cep.length != 8) {
          alert('CEP incorreto, tente novamente com um cep correto')
          event.preventDefault()
          
        }

          await axios.get('https://viacep.com.br/ws/'+cep+'/json/').then((resp)=> {
            

            this.response = resp.data
            this.status = !this.status

            if (this.status == true){
              this.status == false
              this.msg = 'Limpar'
              
            }
            else{
              this.msg = 'Verificar CEP'
              this.cep = ''
            }
            
          }
          )
            
      }
      

   }}

  
   

</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  
}
#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1{
  
}

.form {
  padding: 20px;
  
  
}
.form input {
  margin: 50px;
  padding: 20px;
  border-radius: 40px;
  text-align: center;
  background-color: rgba(68, 68, 68, 0.3);
  font-weight: 700;
}
.pesquisa{
  padding: 10px;
  text-align: center;
  font-size: 90%;
  font-weight: bolder;
}
.button {
  background-color: rgb(17, 175, 2);
  color: rgb(37, 37, 37);
  font-weight: bolder;
  padding: 10px;
}
</style>
