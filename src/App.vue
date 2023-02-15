<template>
  <div class="corpo">
    <nav>
      <ul>
        <li v-for="route in routes">
          <router-link :to="route.path ? route.path : '/'">{{ route.titulo }}</router-link>
        </li>
      </ul>
    </nav>

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

export default {
  data() {
    return {
      routes
    };
  },
  components: { transform }
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