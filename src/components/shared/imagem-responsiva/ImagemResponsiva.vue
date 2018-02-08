<template>
    <img class="imagem-responsiva" :src="url" :title="titulo">
</template>

<script>
export default {
    props: ['url', 'titulo'] 
}
</script>

<style scope>
.imagem-responsiva {
  width: 100%;
}
</style>