<template>
  <div class="corpo">
  
      <meu-menu :rotas="routes"></meu-menu>

      <router-view v-slot="{ Component }">
        <transition name="pagina">
          <component :is="Component" />
        </transition>
      </router-view>

  </div>
</template>



<script>
import { transform } from '@vue/compiler-core';
import { routes } from './routes';
import Menu from './componentes/shared/menu/Menu.vue'

export default {
  components: { 
    'meu-menu': Menu
   },

  data() {
    return {
      routes
    }
  }
  
  }

</script>



<style>
.corpo {
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}
  
.pagina-enter-active, .pagina-leave-active {
  transition: opacity .3s;
}
.pagina-enter, .pagina-leave-active {
  opacity: 0;
}

</style>