<script setup>
import OffcanvasConteudo from './OffcanvasConteudo.vue'
//import Main from './Main.vue';
import Sobre from './Sobre.vue';
import { ref, onMounted, computed} from 'vue'

const dados = ref({});


//onMounted(() => {
//    fetch('http://localhost:8000/api/dicionario')
//   .then(response => response.json())
//    .then(dad => {
//        dados.value = dad;        
//    })
//});

const nome = ref('');

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
    <!-- HEADER -->

    <header id="header">
        <nav class="nav-header">

            <div class="logo">
                <!--<h1>Dicionário Tecnico</h1> -->
            </div>

            <div class="search">
                <input type="text" v-model="nome" id="saida" placeholder="Pesquisar ">
                <button type="button" @click="pesquisaInformacoes">
                    <img src="/public/fontes/Vector.svg" alt="vector">
                </button>
            </div>

            <div class="row" style="margin-top: 18px;">
                <div class="col-md-6">
                    <div class="col-md-5">
                        <button class="btn" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasExample"
                            aria-controls="offcanvasExample">
                            <!--<img src="../assets/icons8-menu-do-xbox-64.png" width="40" alt=""> -->

                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48" width="39px" height="39px">
                                <path fill="#607D8B" d="M6 22H42V26H6zM6 10H42V14H6zM6 34H42V38H6z" />
                            </svg>
                        </button>
                    </div>

                    <OffcanvasConteudo />

                </div>


                <Sobre />

            </div>
        </nav>
    </header>

    <main id="main">
        <section class="container">
            <div class="card cards" id="card">
                <div class="title-text" v-for="d in dados">
                    <h4>{{ d.nome }}</h4>

                    <p>{{ d.descricao }}</p>

                </div>
            </div>
        </section>
    </main>

</template>


<style scoped></style>