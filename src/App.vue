<template>
  <div>
    <Title/>
    <router-view/>
  </div>
</template>

<script>
import Title from './components/Title.vue';

export default {
  components:{
    Title
  }
}

</script>
<style lang="scss">
@import './scss/main.scss';
</style>