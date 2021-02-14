<template>
    <button @click="disparaAcao" :class="estiloDoBotao" :type="tipo">{{ rotulo }}</button>
</template>

<script>
export default {
    props:
    {
        tipo:{
            required:true,
            type:String
        },
        rotulo:{
            required:true,
            type:String
        },
        confirmacao:{
            required:true,
            type:Boolean
        },
        estilo:{
            required:false,
            type:String
        }
    },
    
    methods:{
        disparaAcao:function(){
             console.log(this.confirmacao)
            if(this.confirmacao){
                if(confirm('Confirma operacao?'))
                    return this.$emit('click');
            }
            return this.$emit('click');
        }
    },

    computed:{
        estiloDoBotao(){
            
            if(this.estilo=='padrao')
                 return 'botao botao-padrao';
            else if(this.estilo=='perigo')
                return 'botao botao-perigo';
            else 
                return 'botao botao-padrao';


        }
    }
}
</script>


<style scoped>
.botao {
        display: inline-block;
        padding: 10px;
        border-radius: 3px;
        margin: 10px;
        font-size: 1.2em;
    }

    .botao-perigo {
        background: firebrick;
        color: white;
    }

    .botao-padrao {
        background: darkcyan;
        color: white;
    }

</style>