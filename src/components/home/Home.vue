<template>
<div class="corpo">
  <h1 class="centralizado" v-meu-transform.animate>Alurapic</h1>

  <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre por parte do título">
  
  <ul class="lista-fotos">
    <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
      <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo" v-meu-transform:scale.animate="1.1"/>
          <meu-botao 
            rotulo="remover" 
            tipo="button" 
            @botaoAtivado="remove(foto)" 
            :confirmacao="true"
            estilo="perigo"/>
      </meu-painel>
    </li>
  </ul>
  
</div>
</template>

<script>
import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';

export default {
  components: {
    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva,
    'meu-botao': Botao
  },
  methods: {
    remove(foto) {
      alert('Remover foto ' + foto.titulo);
    }
  },
  data() {
    return {
      fotos: [],
      filtro: ''
    };
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },
  created() {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>

<style>
.centralizado {
  text-align: center;
}
.lista-fotos {
  list-style: none;
}
.lista-fotos .lista-fotos-item {
  display: inline-block;
}
.imagem-responsiva {
  width: 100%;
}
.filtro {
  display: block;
  width: 100%;
}
</style>
