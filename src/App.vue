<template>
  <div class="input-label">
    <label>Cantidad</label> <br />
    <input
      placeholder="Cantidad"
      v-model="Cantidad"
      @keyup.enter="Contar"
      type="number"
    />
  </div>

  <div class="input-label">
    <label>Código de barras</label> <br />
    <input
      ref="focusMe"
      placeholder="Codigo de barras"
      v-model="Codigo"
      @keyup.enter="Contar"
    />
  </div>

  <button class="contar" @click="Contar()">Contar</button>

  <div id="tabla">
    <table>
      <tr>
        <th>Cantidad</th>
        <th>Codigo</th>
      </tr>
      <tr v-for="todo in inventario">
        <td>{{ todo.cantidad }}</td>
        <td>{{ todo.codigo }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      Cantidad: 1,
      Codigo: null,
      inventario: [],
    };
  },
  mounted() {
    this.$refs.focusMe.focus();
  },
  methods: {
    Contar() {
      if (this.Codigo == null || this.Codigo == "") {
        alert("El codigo debe tener valor ");
        return;
      }

      if (0 >= this.Cantidad) {
        alert("La cantidad debe ser mayor a 0");
        return;
      }

      let existeCodigo = this.inventario.find((x) => x.codigo == this.Codigo);

      if (existeCodigo) {
        let d = this.inventario.findIndex((x) => x.codigo == this.Codigo);
        this.inventario[d].cantidad =
          this.inventario[d].cantidad + this.Cantidad;
      } else {
        let nuevo = { cantidad: this.Cantidad, codigo: this.Codigo };
        this.inventario.push(nuevo);
      }

      //Se reinicia
      this.Cantidad = 1;
      this.Codigo = "";
      this.$refs.focusMe.focus();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  margin: 5px;
}

.input-label {
  display: inline-block;
}

table,
th,
td {
  border: 1px solid black;
}

#tabla {
  margin: 15px;
}

.contar {
  color: white;
  background-color: #252440;
  padding: 7px;
  margin: 4px;
  border-radius: 3px;
  border-color: #252440;
}
</style>
