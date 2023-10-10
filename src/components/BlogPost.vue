<script setup>
    //defineProps(['title'])
    //como objeto
    //const props = defineProps(['title'])
    //acederiamos como props.tittle  
    //ahora con un objeto 
    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin descripcion',
        },
    });
</script>
<template>
    <div class="cuadro">
        <h1> {{id}}-{{ title }} </h1>
        <p> {{ body }} </p>
        <button @click="$emit('evento',title)">Favorito</button>
    </div>
</template>
<style>
.cuadro{
    border: 2px solid white;
}
</style>