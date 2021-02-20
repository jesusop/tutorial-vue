<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <formulario-persona @add-persona="agregarPersona" />
        <tabla-personas
          :personas="personas"
          @delete-persona="eliminarPersona"
          @actualizar-persona="actualizarPersona"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from "@/components/TablaPersonas.vue";
import FormularioPersona from "@/components/FormularioPersona.vue";

export default {
  name: "app",
  components: {
    TablaPersonas,
    FormularioPersona
  },
  methods: {
    agregarPersona(persona) {
      let id = 0;

      if (this.personas.length > 0) {
        id = this.personas[this.personas.length - 1].id + 1;
      }
      this.personas = [...this.personas, { ...persona, id }];
    },
    eliminarPersona(id) {
      this.personas = this.personas.filter(persona => persona.id !== id);
    },
    actualizarPersona(id, personaActualizada) {
      this.personas = this.personas.map(persona =>
        persona.id === id ? personaActualizada : persona
      );
    }
  },
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: "Hector",
          apellido: "GA",
          email: "hec@email.com"
        },
        {
          id: 2,
          nombre: "Walter",
          apellido: "GA",
          email: "wal@email.com"
        },
        {
          id: 4,
          nombre: "Jesus",
          apellido: "Ovalle",
          email: "jesus@email.com"
        }
      ]
    };
  }
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
</style>
