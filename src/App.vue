<template>
  <div id="app" class="container">
    <!-- Panel de configuración -->
    <div class="config-panel">
      <label>
        Color de fondo:
        <input type="text" v-model="backgroundColor" placeholder="Ej: darkgreen" />
      </label>

      <label>
        Color de texto:
        <input type="text" v-model="textColor" placeholder="Ej: white" />
      </label>

      <label>
        Mostrar texto:
        <input type="checkbox" v-model="showText" />
      </label>

      <label>
        Borde:
        <input type="range" min="0" max="50" v-model="borderRadius" />
      </label>

      <label>
        Contenido textual:
        <input type="text" v-model="textContent" placeholder="Awesome Vue.js" />
      </label>

      <label>
        Tipografía:
        <select v-model="fontFamily">
          <option v-for="font in fonts" :key="font" :value="font">{{ font }}</option>
        </select>
      </label>

      <label>
        Opaco:
        <input type="checkbox" v-model="isOpaque" />
      </label>

      <fieldset>
        <legend>Tamaño de letra:</legend>
        <label>
          <input type="radio" value="small" v-model="fontSize" /> Pequeño
        </label>
        <label>
          <input type="radio" value="medium" v-model="fontSize" /> Mediano
        </label>
        <label>
          <input type="radio" value="large" v-model="fontSize" /> Grande
        </label>
      </fieldset>
    </div>

    <!-- Figura dinámica -->
    <div
      v-show="isVisible"
      class="figure"
      :style="figureStyle"
      :class="{ opaque: isOpaque }"
    >
      <span v-if="showText">{{ textContent }}</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Estado inicial de los inputs
      backgroundColor: "darkgreen",
      textColor: "white",
      showText: true,
      borderRadius: 25,
      textContent: "Awesome Vue.js",
      fontFamily: "sans-serif",
      fonts: ["sans-serif", "serif", "cursive", "monospace"],
      isOpaque: false,
      fontSize: "medium",
      isVisible: true,
    };
  },
  computed: {
    // Estilos dinámicos para la figura
    figureStyle() {
      return {
        backgroundColor: this.backgroundColor,
        color: this.textColor,
        borderRadius: `${this.borderRadius}px`,
        fontFamily: this.fontFamily,
        fontSize: this.fontSize === "small" ? "12px" : this.fontSize === "medium" ? "16px" : "20px",
        width: "200px",
        height: "200px",
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        textAlign: "center",
        transition: "all 0.3s ease",
      };
    },
  },
};
</script>

<style>
.container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.config-panel {
  background: #2c3e50;
  color: white;
  padding: 20px;
  border-radius: 10px;
  width: 40%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.config-panel input,
.config-panel select {
  margin-top: 5px;
  padding: 5px;
  width: 100%;
}

.config-panel fieldset {
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
}

.figure {
  border: 2px solid #ccc;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
}

.opaque {
  opacity: 0.5;
}
</style>
