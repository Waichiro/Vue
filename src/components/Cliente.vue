<template>
    <div :class="{'Cliente': !isPremiun, 'ClientePremiun': isPremiun}" >
        <h4>Nome: {{ cliente.nome | processarNome }}</h4>
       
        <p>Descrição: {{ cliente.descricao }}</p>
       
        <p v-if="showNumero === false" >Numero: {{ cliente.numero }}</p>
        <p v-else>O usuario escondeu o numero</p>
        <hr>
        <button @click="mudarCor()" class="button is-primary">Mudar classe</button>
        <button @click="emitirEventoDelete()" class="button is-danger">Deletar</button>
        <hr>
        <h4>IdEspecial: {{ idEspecial }}</h4>
    </div>
    
</template>

<script>

export default ({
    data(){
        return {
              
            isPremiun: false
           
        }
    },
    props:{
        
        cliente: Object,
        showNumero: Boolean
    },
    methods: {
        mudarCor: function(){
            this.isPremiun = !this.isPremiun;
        },
        emitirEventoDelete: function(){
            console.log("Emitindo do filho");
            this.$emit("meDelete", {idDoCliente: this.cliente.id, component: this});
        }
    },
    filters: {
        processarNome: function(value){
            return value.toUpperCase();
        }
    },
    computed: {
        idEspecial: function(){
            return "#" + (this.cliente.nome + this.cliente.numero ).toUpperCase();
        } 
    }

})
</script>

<style scoped>
    .Cliente {
        background-color: #ECE5E3;
        max-width: 600px;
        height: 250px;
        padding: 1%;
        margin-top: 2%;
    }

    .ClientePremiun{
        background-color: black;
        color: yellow;
        max-width: 600px;
        height: 250px;
        padding: 1%;
        margin-top: 2%;
    }
</style>
