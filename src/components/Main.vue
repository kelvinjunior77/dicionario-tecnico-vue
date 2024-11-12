<script setup>
import { ref, onMounted } from 'vue'

const dados = ref({});

//onMounted(() => {
//    fetch('http://localhost:8000/api/dicionario')
 //   .then(response => response.json())
//    .then(dad => {
//        dados.value = dad;        
//    })
//});

//const pessoa = ref({}); = dados
const nome = ref(''); //codigoUsuario

//const habilitaBotao = computed(() => codigoUsuario.value > 0);

const pesquisaInformacoes = async () => {
    dados.value = await buscaInformacoes(nome.value);
    
}

onMounted(async () => {
  dados.value = await buscaInformacoes();
});     

const buscaInformacoes = async (d) => { 
    fetch(`http://localhost:8000/api/dicionario/search/${d}`)
    .then(response => response.json())
    .then(r => {
        dados.value = r;
    })
};

</script>

<template>
   <main id="main">
        <section class="container">
            <div class="card card" id="card">
                <div class="title-text" v-for="d in dados">
                        <h4>{{ d.nome }}</h4>
                    <hr>
                        <div class="card-body d-none">
                            <p>{{ d.descricao }}</p>
                        </div>
                </div>
            </div>
        </section>
    </main>
</template>