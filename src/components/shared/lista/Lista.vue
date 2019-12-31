<template>
  <div class="lista">
    <h2 class="lista-titulo">{{titulo}}</h2>
    <slot class="lista-corpo">
      
    </slot>
  </div>
</template>

<script>
export default {
    props: ['titulo']
};
</script>

<style scoped>
/* estilo do painel */
.imagem-responsiva {
  width: 100%;
}
.lista {
  padding: 0 auto;
  border: solid 1px grey;
  display: inline-block;
  margin: 0 10px;
  box-shadow: 2px 2px 10px grey;
  width: 150px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}
.lista .lista-titulo {
  font-size: 14px;
  text-align: center;
  border-bottom: solid 1px grey;
  background: mediumspringgreen;
  margin: 0;
  padding: 10px;
  text-transform: uppercase;
}
</style>