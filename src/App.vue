<script setup>
//reactividad
import {ref,computed} from 'vue'
import BlogPost from './components/BlogPost.vue';
import buttonCounter from './components/ButtonCounter.vue'

  const name = "Vue dinamico";
  const color = "color: blue";
  const array = ["blue","white","black"];
  const activo = true;
  const arrayfrutas = [
    {
      name: "manzana",
      price: "$1.00",
      description: "una manzana",
    },
    {
      name: "Pera",
      price: "$2.00",
      description: "una pera",
    },
    {
      name: "Naranja",
      price: "$3.00",
      description: "una naranja",
    },
  ];
  const objeto = {
    name: "manzana",
    price: "$1.00",
    description: "una manzana",
  }
  //funcion de flecha
  const click= () => {
    console.log("me diste click")
  }
  //funcion de flecha con parametros
  const clickk = (mensage) => {
    console.log(mensage)
  }
  const counter = ref(0);
  const increment = () =>{
    counter.value++;
  }
  //computed es una funcion que realiza calculos pero siempre debe retornal algo es como un method
  const classcount = computed(() =>{
      if (counter.value<0){
        return 'negativo'
      }
      else if(counter.value>0){
        return 'positivo'
      }else{
        return 'cero'
      }
    }
  )
  //Aqui comiensa codigo para sesion de componentes
  const posts = ref([
    { title: 'Post 1', id: 1, body: 'Descripcion 1'},
    { title: 'Post 2', id: 2, body: 'Descripcion 2'},
    { title: 'Post 3', id: 3, body: 'Descripcion 3'},
    { title: 'Post 4', id: 4},
  ]);

  const fav = ref("");
  const cambiarfav = (title) => {
    fav.value=title;
  };
</script>

<template>
  <!DOCTYPE html>
  <html lang="es">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
    <!-- v-bind-->
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :style="color">soy azul</h2>
    <h3>{{ array }}</h3>
    <h4 :style="`color: ${array[1]}`"> que onda </h4>
    <h2> {{ activo ? 'Esto activo': 'Estoy inactivo'}}</h2>
    <!--directivas-->
    <h3 v-if="activo">hola estoy activo</h3>
    <h2 v-else-if="activo === false"> hola estoy inactivo</h2>
    <h2 v-else>hola estoy inactivo</h2>
    <h3 v-if="!activo">hola estoy inactivo</h3>
    <h1 v-show="activo">Hola estoy activo</h1> <!--solo cambia el display:none-->
    <!--v-for objetos-->
    <ul>
      <li v-for="color in array">{{ color }}</li>
    </ul>
    <!--con index-->
    <ul>
      <li v-for="(color,index) in array" :key="index"> {{index}} - {{ color }} </li>
    </ul>
    <!--v-for con un array de objetos-->
    <ul>
      <li v-for="fruta in arrayfrutas" :key="fruta.name">{{fruta.name}} - {{fruta.price}} - {{fruta.description}}</li>
    </ul>
    <!--v-for con un objeto-->
    <ul>
      <li v-for="(value,propiedad, index) in objeto" :key="value">{{ propiedad}} : {{ value }}</li>
    </ul>
    <!--vfor y vif-->
    <ul>
      <template v-for="fruta in arrayfrutas" :key="fruta.name">
        <li v-if="fruta.name === 'manzana'"> {{fruta.name}} - {{fruta.price}} - {{fruta.description}}</li>
      </template>
    </ul>
    <!--v-on-->
    <button @click="click">dame click</button>
    <button @click="clickk('hola')">dame click</button>
    <!--con botones especificos-->
    <button @click.right="click">Right</button>
    <button @click.middle="click">Middle</button>
    <!--ractividad como modificar la pagina con cambios en variables de javascript-->
    <h1>{{ counter }}</h1>
    <button @click="increment">aumentar</button>  
    <!--las clases pueden ser dinamicas-->
    <h1 :class="counter > 0 ? 'positivo' : 'negativo'"> {{ counter }}</h1>
    <h1 :class="classcount"> {{ counter }}</h1>
    <!--Parte de Componentes-->
    <h1>APP</h1>
  <h2>Mi post Favorito: {{fav}}</h2>
  <buttonCounter/>
  <!--<BlogPost title="Post 1" :id="1"/>mandar un parametro-->
  <BlogPost v-for="post in posts" 
  :key="post.id" 
  :title="post.title" 
  :id="post.id" 
  :body="post.body"
  @evento="cambiarfav"></BlogPost>
  </body>
  </html>
</template>
<style>
.positivo{
  color: green;
}
.negativo{
  color: red;
}
.cero{
  color: white;
}
</style>