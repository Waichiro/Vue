<template>
  <div id="app" >

    <h3>Cadastro: </h3>
    <small id="nomeErr" v-show="deuNomeErro">O nome é invalido</small><br>
    <input type="text" placeholder="Nome" class="input is-success" v-model="nomeField"><br>
    
    <input type="text" placeholder="Descricao" class="input is-success" v-model="descricaoField"><br>
    
    <input type="number" placeholder="Numero" class="input is-success" v-model="numeroField"><br><br>
    <button @click="cadastrarUsuario" class="button is-primary">Cadastrar</button>
    <hr>
    <div v-for="(cliente) in ordenarClientes"  :key="cliente.id">
      
      <Cliente :cliente="cliente" @meDelete="deletarusuario($event)"/>
      
    </div>
    
  </div>
</template>

<script>
import _ from 'lodash';
import Cliente from './components/Cliente.vue'

export default {
  name: 'App',
  data(){
    return{

      deuNomeErro: false,
     
      nomeField: "",
      descricaoField: "",
      numeroField: "",
      clientes: [
        {
          id: 1,
          nome: "Waichiro",
          descricao: "Oi meu nome é Waichiro",
          numero: "25465546"
        },
        {
          id: 2,
          nome: "Xoao",
          descricao: "Oi meu nome é Xoao",
          numero: "6.7496."
        },
        {
          id: 3,
          nome: "Zafael",
          descricao: "Oi meu nome é Zafael",
          numero: "6456465"
        }
      ]
    }

  },
  components: {
    Cliente
  },
  methods: {
    cadastrarUsuario: function(){
      if(this.nomeField == "" || this.nomeField == " " || this.nomeField < 3){
        this.deuNomeErro = true;
      }else{
        this.clientes.push({nome: this.nomeField, descricao: this.descricaoField, numero: this.numeroField, id: Date.now()});
        this.nomeField = "",
        this.descricaoField = "",
        this.numeroField = ""
        this.deuNomeErro = false;
      }
    
      
    },
    deletarusuario: function($event){
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
    }
  }, 
  computed: {
    ordenarClientes: function(){
      return _.orderBy(this.clientes,['nome'], ['asc']);
    }
  }
};
</script>

<style>

  #nomeErr{
    color: red;
  }

</style>
