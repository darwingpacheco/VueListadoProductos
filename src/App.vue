<script setup>
import { ref } from 'vue';

const productos = ref([
  { nombre: 'Producto 1', cantidad: 10, valor: 5000, diasRestantes: 0 },
  { nombre: 'Producto 2', cantidad: 0, valor: 1000, diasRestantes: 0 },
  { nombre: 'Producto 3', cantidad: 5, valor: 20000, diasRestantes: 2 },
  { nombre: 'Producto 4', cantidad: 10, valor: 500, diasRestantes: 5 },
  { nombre: 'Producto 5', cantidad: 0, valor: 1000, diasRestantes: 0 },
  { nombre: 'Producto 6', cantidad: 25, valor: 200, diasRestantes: 0 },
  { nombre: 'Producto 7', cantidad: 40, valor: 500, diasRestantes: 5 },
  { nombre: 'Producto 8', cantidad: 0, valor: 1000, diasRestantes: 0 },
  { nombre: 'Producto 9', cantidad: 6, valor: 20000, diasRestantes: 2 },
  // Agrega más productos aquí según tus necesidades
]);

const nuevoProducto = ref({
  nombre: '',
  cantidad: 0,
  valor: 0,
  diasRestantes: 0
});

function productosVencer(producto) {
  return producto.diasRestantes <= 0;
}

function cantidadTotalProductos() {
  return productos.value.reduce((total, producto) => {
    return producto.cantidad > 0 ? total + 1 : total;
  }, 0);
}

function valorTotal() {
  return productos.value.reduce((total, producto) => {
    return producto.cantidad > 0 ? total + producto.valor : total;
  }, 0);
}

function agregarProducto() {
  productos.value.push({
    nombre: nuevoProducto.value.nombre,
    cantidad: nuevoProducto.value.cantidad,
    valor: nuevoProducto.value.valor,
    diasRestantes: nuevoProducto.value.diasRestantes
  })
}
</script>
<template>
  <header>
    <div>
      <h1>Listado de Productos</h1>
      <table>
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Cantidad</th>
            <th>Valor</th>
            <th>Días restantes para vencer</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="producto in productos" :key="producto.nombre" v-show="producto.cantidad !== 0" :class="{'vencido': productosVencer(producto)}">
            <td>{{ producto.nombre }}</td>
            <td>{{ producto.cantidad }}</td>
            <td>{{ producto.valor }}</td>
            <td>{{ producto.diasRestantes }}</td>
            <td v-if="productosVencer(producto)" class="vencido">VENCIDO!</td>
          </tr>
        </tbody>
      </table>
      <p>Total de productos: {{ cantidadTotalProductos() }}</p>
      <p>Valor total: {{ valorTotal() }}</p>
    </div><br>
    <div class="agregar">
      <h2>Agregar Producto</h2>
      <form @submit.prevent="agregarProducto">
        <label>
          Nombre:
          <input type="text" v-model="nuevoProducto.nombre" required>
        </label><br>
        <label>
          Cantidad:
          <input type="number" v-model="nuevoProducto.cantidad" required>
        </label><br>
        <label>
          Valor:
          <input type="number" v-model="nuevoProducto.valor" required>
        </label><br>
        <label>
          Días restantes para vencer:
          <input type="number" v-model="nuevoProducto.diasRestantes" required>
        </label><br>
        <button class="button" type="submit">Agregar</button>
      </form>
    </div>
  </header>
</template>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 11px;
  border-bottom: 1px solid #ddd;
  align-items: center;
}

th {
  background-color: black;
  font-weight: bold;
}
.vencido td {
  background-color: red;
  color: white;
}
</style>

