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

    const guitar = ref({});
	//console.table(guitarras.value[0].id);
	onMounted(() => { 
		guitarras.value = db;
		state.guitarras = db;
        guitar.value = db[2];
	})


    const incrementar = (guitarra) => { 
        const existe = carrito.value.findIndex(producto => producto.id === guitarra.id);
        
        if(existe >= 0) {
            carrito.value[existe].cantidad++;
        } else {
            guitarra.cantidad = 1;
            carrito.value.push(guitarra);
        }
        
    }

    const aumentar = (id) => {
        const index = carrito.value.findIndex(producto => producto.id === id);
        carrito.value[index].cantidad++;
    }

    const decrementar = (id) => {
        const index = carrito.value.findIndex(producto => producto.id === id); // Sirve para encontrar el prodcuto 
        carrito.value[index].cantidad--;
        
    }

    const eliminar = (id) => {
        carrito.value = carrito.value.filter( product => product.id !== id); //Sirve para filtrar el los valores y solo traerte los que cumplent con la condicion
    }

    const vaciar = () => {
        carrito.value = [];
    }

    

</script>

<template>
    <Header v-bind:carrito="carrito" v-bind:guitar="guitar" @aumentar="aumentar" @decrementar="decrementar" @eliminar="eliminar" @vaciar = "vaciar"></Header>

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



