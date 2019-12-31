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
.lista {
  padding: 0 auto;
  display: inline-block;
  margin: 20px;
  box-shadow: 2px 2px 10px grey;
  width: 250px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}
.lista .lista-titulo {
  font-size: 18px;
  text-align: center;
  border-bottom: solid 1px grey;
  background: #333;
  color: #F1F1F1;
  margin: 0;
  padding: 10px;
  text-transform: uppercase;
  border-top-right-radius: 6px;
  border-top-left-radius: 6px;
}
</style>