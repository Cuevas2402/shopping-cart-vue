<script setup>
	import {ref, reactive, onMounted} from 'vue';
	import { db} from'./data/data.js';
	import Guitar from './components/guitar.vue'
    import Header from './components/header.vue'
	const state = reactive({
		guitarras: db
	});

    const carrito = ref([]);

	const guitarras = ref(db);
	//console.table(guitarras.value[0].id);
	onMounted(() => { 
		guitarras.value = db;
		state.guitarras = db;
	})


    const incrementar = (guitarra) => { 
        const existe = carrito.value.findIndex(producto => producto.id === guitarra.id);
        if(existe){
            carrito.value.push(guitarra);
        }
        
    }

    

    

</script>

<template>
    <Header v-bind:carrito="carrito"></Header>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitar v-for="guitarra in guitarras" v-bind:guitarra="guitarra" @incrementar="incrementar" ></Guitar>
        </div>
    </main>


    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>
</template>



