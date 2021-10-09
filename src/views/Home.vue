<template>
  <header>
    <h1>{{ titulo }}</h1>
  </header>

  <main>
    <div>
      <h2>Registrar Eventos</h2>
      <form id="formulario_evento" action="#" method="post">
        <label for="cliente">Cliente:</label>
        <!-- <input type="text" name="cliente" /> -->

        <!-- v-model -->
        <input type="text" name="cliente" v-model="evento.cliente">
        <!-- v-model se coloca en el input -->
        <!-- dentro de v-model voy a colocar la variable que uiero que se este escuchando -->

        <label for="documento">Documento:</label>
        <input type="text" name="documento" v-model="evento.documento" />

        <label for="salon">Salon</label>
        <div>
          <input type="radio" name="salon" value="1" v-model="salon" id="" /> Normal
          <input type="radio" name="salon" value="2" v-model="salon" id="" /> Grande
        </div>

        <label for="meseros_extra">Agregar meseros extra?</label>
        <input type="checkbox" name="meseros_extra" v-model="extra" value="Si" id="" />

        <!-- v-if -->
        <!-- Me muestra la etiqueta si se cumple la condicion que se coloca entre las comillas -->
        <label v-if="extra" for="cantidad">Cantidad Meseros</label>
        <input v-if="extra" type="number" name="cantidad" />

        <label for="servicio_comida">Incluir Comida</label>
        <input type="checkbox" name="servicio_comida" value="Si" id="" />

        <label for="platos">Cantidad Platos</label>
        <input type="number" name="platos" />

        <button type="reset" name="limpiar">Limpiar</button>

        <!-- <button onclick="procesarInformacion()" type="button"> -->
          <!-- en lugar de onclick se maneja v-on -->
          <!-- v-on = @ se puede reemplazar por la arroba@ -->
          <!-- <button v-on:click="procesarInformacion()" type="button"> -->
          <button @click.prevent="procesarInformacion()" type="button">

          Agregar Evento
        </button>
      </form>

      <!-- ejemplo de reactividad -->
      <!-- repite lo que estoy escribiendo -->
      <!-- <h2>Cliente: {{evento.cliente}}</h2> -->
      <h2>salon: {{salon}}</h2>

    </div>

    <div>
      <h2>Listado de Eventos</h2>
      <table border="1">
        <thead>
          <tr>
            <th>CLIENTE</th>
            <th>SALON</th>
            <th>MESEROS</th>
            <th>PLATOS</th>
            <th>TOTAL</th>
          </tr>
        </thead>
        <tbody id="datos_eventos">
          <!-- <v-for> -->
          <!-- es un for de javascript -->
          <!-- la key es obligatoria -->
          <!-- <tr v-for="unEvento in listaEventos" :key="unEvento"> -->
          <tr v-for="unEvento in listaEventos" v-bind:key="unEvento">
            <!-- v-bind: v-bind me va a permitir colocar cualquier variable que haya definido dentro de data -->
            <!-- v-bind:key es lo mismo que :key -->
            <td>{{ unEvento.cliente }}</td>
            <td>{{ unEvento.salon.nombre }}</td>
            <td>{{ unEvento.meseros }}</td>
            <td>{{ unEvento.platos }}</td>
            <td>{{ unEvento.total }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

// export default {
//   name: 'Home',
//   components: {
//     HelloWorld
//   }
// }

export default {
  data() {
    return {
      titulo: "Gestion de eventos",

        salonNormal : { "nombre": "Normal", "precio": 1000000, "extra_mesero": 150000, "cantidad_meseros": 1, "plato": 50000 },
        salonGrande : { "nombre": "Grande", "precio": 2000000, "extra_mesero": 100000, "cantidad_meseros": 4, "plato": 40000 },
      
      listaEventos: [
        {
          cliente: "Jose",
          documento: "74989898",
          meseros: 2,
          platos: 150,
          salon: "Normal",
          total: 3200000,
        },
      ], //lista

      evento: {
        cliente:"",
        documento:"",
        salon:{},
        meseros:0,
        platos:0,
        total:0,


      }, //diccionario que me va a guardar toda la informacion del formulario

      salon:0,
      extra:true,
      comida:false,


    }; //Cierre return
  }, //Cierre data

  name: "Home",
  components: {},

  // Atributo methods
  // aqui se definen los diferentes metodos y funciones
  // si yo quiero referirme a una variable que este dentro de dat debo usar el this.

  methods:{
    procesarInformacion(){
      // console.log(this.evento);

    } // cierre procesarInformacion

  } // cierre methods


}; //Cierre export default
</script>


<style scoped>
body {
  padding: 2rem;
}

#formulario_evento {
  display: grid;
  grid-template-columns: 7.2rem 12rem;
  padding: 1rem;
  row-gap: 1rem;
  column-gap: 0.5rem;
}

main {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 1rem;
}

table {
  width: 80%;
  margin: 0 auto;
}

table td {
  text-align: center;
}
</style>
