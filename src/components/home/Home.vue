<template>
<div>
  <h1 class="centralizado">{{ h1 }}</h1>

  <input type="search" class="filtro" placeholder="filtrar por titulos comecando ou terminando com..." v-on:input="filtro = $event.target.value">
  <h4 v-show="isH4FiltroShow">Filtrando pipeline com: {{ filtro }}</h4>

  <ul class="lista-fotos">
    <li class="lista-fotos-item" v-for="foto of fotosComFiltros">

     <meu-painel :titulo="foto.titulo"> 
      <imagem-responsiva :url="foto.url" :titulo="foto.titulo" >
      </imagem-responsiva>
      <meu-botao tipo="button" rotulo="REMOVER" v-on:click="remove(foto)" :confirmacao="true"
      estilo="perigo"/>
     </meu-painel>
      
    </li>
  </ul>
  <h2 v-text="h2"></h2>
  
 
</div>

</template>

<script>
import Painel from '../shared/painel/Painel.vue'
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue'
import Botao from '../shared/botao/Botao.vue';
export default {

  components:{
    'meu-painel':Painel,
    'imagem-responsiva':ImagemResponsiva,
    'meu-botao':Botao
   
  },

 data(){
   return{
    h1:"Pictures",
    h2:"Oracle Certified Professional JSE 11.",
    fotos:[],
    filtro:"",
    isH4FiltroShow : false
 }
 },
 created(){
   
   let promise = this.$http.get("http://localhost:3000/v1/fotos");
   promise.then(res => res.json()).then(fotos => { console.log(fotos.content);this.fotos=fotos},err => console.log(err));
  },
  computed:{

    fotosComFiltros(){
      if(this.filtro.length==0){
         this.isH4FiltroShow = false;
        return this.fotos
     } else{
        this.isH4FiltroShow = true;
       return this.fotos.filter(value=> value.titulo.toLowerCase().startsWith(this.filtro.toLowerCase()) || value.titulo.toLowerCase().endsWith(this.filtro.toLowerCase()));
      }
    }
  },
  methods:{

    remove : function(foto){
        alert("Remover a foto " + foto.titulo);
      }
      
    
  }
 }

</script>

<style>

 

  .centralizado{
    text-align: center;
  } 

  .lista-fotos{
    list-style-type: none;
  }

   .lista-fotos-item{
    display: inline-block;
  }

 .filtro{
   display: block;
   width: 100%;
 }
</style>
