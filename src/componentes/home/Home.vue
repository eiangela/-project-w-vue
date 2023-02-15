<template>
    <div>
      <h1 class="centralizado"> {{ titulo }} </h1>
      <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre por parte do titulo">
    
      <ul class="lista-fotos">
        <li class="lista-fotos-item" v-for="foto in fotosComFiltro">
  
            <meu-painel :titulo="foto.titulo">
              <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
            </meu-painel>
      
        </li>
  
      </ul>
  
    </div>
  </template>
  
  
  
  <script>
  import Painel from '../shared/painel/Painel.vue';
  import imagemResponsiva from '../shared/imagem-responsiva/imagemResponsiva.vue';
  export default {
  
    components: {
      'meu-painel': Painel,
      'imagem-responsiva': imagemResponsiva
    },
  
    data() {
  
      return {
  
        titulo: 'Alurapic',
        fotos: [],
        filtro:''
      }
    },
  
    computed: {
      fotosComFiltro() {
        if(this.filtro) {
          let exp = new RegExp(this.filtro.trim(), 'i');
          return this.fotos.filter(foto => exp.test(foto.titulo));
        } else {
          return this.fotos;
        }
      }
      
    },
  
    created() {
  
      //let promise = this.$http.get('http://localhost:3000/v1/fotos');
      //promise.then(res => console.log(res));
  
      const fetchData = fetch('http://localhost:3000/v1/fotos', { method: 'GET' })
        .then((response) => response.json())
        .then((data) => {
          data.shift();
          this.fotos = data;
          console.log(data);
        });
  
  
    },
  
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
  
  
  
  .filtro {
    display: block;
    width: 100%;
  }
  
  </style>
  