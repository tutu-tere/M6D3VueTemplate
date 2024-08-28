<script>
export default {
  name: 'FormRendering',
  data() {
    return {
      colorFondo: '',
      colorTexto: '',
      mostrar: '',
      borde: '',
      contenido: '',
      opaco: '',
      tipoLetraSelected: '',
      tipoLetra: ['monospace', 'serif', 'sans-serif'],
      tamanoLetraSelected: '',
      tamanoLetra: [
        { value: '2rem', label: 'Pequeño' },
        { value: '5rem', label: 'Mediano' },
        { value: '8rem', label: 'Grande' }
      ]
    }
  }
}
</script>
<template>
  <div class="container">
    <!-- Bloque Izquierda -->
    <form class="form flex-column">
      <!-- Color Fondo -->
      <div class="form-group">
        <label for="fondo">Color de fondo</label>
        <input type="color" id="fondo" v-model="colorFondo" class="form-control" />
      </div>
      <!-- Color Texto -->
      <div class="form-group">
        <label for="colorTexto">Color de texto</label>
        <input type="color" id="colorTexto" v-model="colorTexto" class="form-control" />
      </div>
      <!-- Mostrar Texto -->
      <div class="form-group flex-row">
        <label for="mostrarTexto">Mostrar texto</label>
        <input type="checkbox" id="mostrarTexto" v-model="mostrar" />
      </div>
      <!-- Borde -->
      <div class="form-group">
        <label for="borde">Borde</label>
        <input type="range" name="borde" id="borde" min="0" max="50" v-model="borde" />
      </div>
      <!-- Contenido -->
      <div class="form-group flex-column">
        <label for="contenido">Contenido</label>
        <textarea id="contenido" v-model="contenido"></textarea>
      </div>
      <!-- Tipografía -->
      <div class="form-group">
        <label for="tipografia">Tipografía</label>
        <select name="tipo" id="tipografia" v-model="tipoLetraSelected">
          <option v-for="tipografia in tipoLetra" :key="tipografia" :value="tipografia">
            {{ tipografia }}
          </option>
        </select>
      </div>
      <!-- opaco -->
      <div class="form-group flex-row">
        <label for="opaco">Opaco</label>
        <input type="checkbox" id="opaco" v-model="opaco" />
      </div>
      <!-- Tamaño Letra -->
      <div class="form-group flex-row">
        <label for="tamañoLetra">Tamaño Letra</label>

        <div class="check-item flex-row" v-for="tamano in tamanoLetra" :key="tamano.value">
          <label :for="tamano.value">{{ tamano.label }}</label>
          <input
            type="radio"
            :name="tamano.value"
            :value="tamano.value"
            :id="tamano.value"
            v-model="tamanoLetraSelected"
          />
        </div>
      </div>
    </form>
    <!-- Bloque Derecha -->
    <div
      id="resultado"
      :style="{
        backgroundColor: colorFondo,
        color: colorTexto,
        borderRadius: `${borde}%`,
        fontFamily: tipoLetraSelected,
        fontSize: tamanoLetraSelected
      }"
      :class="{
        opaco: opaco
      }"
    >
      <p v-show="mostrar">
        {{ contenido }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  /* flex-direction: row; // por defesto */
  align-items: center;
  gap: 2rem;
}

.flex-row {
  display: flex;
  gap: 10px;
}

.flex-column {
  display: flex;
  flex-direction: column;
}

form {
  align-items: start;
  background-color: #2f4f4f;
  padding-inline: 2.5rem;
  padding-block: 2rem;
}

label {
  color: white;
}

input {
  width: 100%;
}

.form-group {
  padding-bottom: 1.5rem;
}

#resultado {
  height: 450px;
  width: 450px;
  display: grid;
  place-content: center;
}

.opaco {
  opacity: 0.5;
}
</style>
