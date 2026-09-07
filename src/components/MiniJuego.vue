<script setup lang="ts">
import { ref, computed } from 'vue';


type Direction = 'adelante' | 'atras' | 'izquierda' | 'derecha';

interface Node {
  id: string;
  text: string;
  paths: Partial<Record<Direction, string>>; // Conexión a otros nodos
}


const nodes: Record<string, Node> = {
  inicio: {
    id: 'inicio',
    text: 'Te encuentras en la entrada de una vieja mazmorra medieval. Un viento frío sopla desde el interior.',
    paths: { adelante: 'pasillo' }
  },
  pasillo: {
    id: 'pasillo',
    text: 'Estás en un pasillo oscuro iluminado por antorchas parpadeantes. Ves puertas a tus lados.',
    paths: { atras: 'inicio', izquierda: 'armeria', derecha: 'biblioteca', adelante: 'cruzamiento' }
  },
  armeria: {
    id: 'armeria',
    text: 'Entras a la armería. Hay espadas oxidadas por el suelo y un cofre de hierro al fondo.',
    paths: { derecha: 'pasillo' }
  },
  biblioteca: {
    id: 'biblioteca',
    text: 'Una biblioteca olvidada. Las estanterías de madera están cubiertas de polvo y tomos antiguos.',
    paths: { izquierda: 'pasillo' }
  },
  cruzamiento: {
    id: 'cruzamiento',
    text: 'Llegas a un cruce. Escuchas un leve susurro que proviene del frente.',
    paths: { atras: 'pasillo', adelante: 'tesoro' }
  },
  tesoro: {
    id: 'tesoro',
    text: '¡Has encontrado la sala del tesoro! Un resplandor dorado ilumina la estancia. Has triunfado.',
    paths: { atras: 'cruzamiento' }
  }
};


const currentNodeId = ref<string>('inicio');
const currentNode = computed(() => nodes[currentNodeId.value]);


const move = (direction: Direction): void => {
  const nextNodeId = currentNode.value.paths[direction];
  if (nextNodeId) {
    currentNodeId.value = nextNodeId;
  }
};
</script>

<template>
  <div class="mud-container">
    <div class="screen">
      <p class="description">{{ currentNode.text }}</p>
    </div>

    <div class="controls">
      <button 
        :disabled="!currentNode.paths.adelante" 
        @click="move('adelante')"
      >
        ▲ Adelante
      </button>
      
      <div class="middle-buttons">
        <button 
          :disabled="!currentNode.paths.izquierda" 
          @click="move('izquierda')"
        >
          ◄ Izquierda
        </button>
        <button 
          :disabled="!currentNode.paths.derecha" 
          @click="move('derecha')"
        >
          Derecha ►
        </button>
      </div>

      <button 
        :disabled="!currentNode.paths.atras" 
        @click="move('atras')"
      >
        ▼ Atrás
      </button>
    </div>
  </div>
</template>

<style scoped>
.mud-container {
  max-width: 500px;
  margin: 0 auto;
  font-family: 'Courier New', Courier, monospace;
  background-color: #0d1117;
  color: #00ff66;
  padding: 20px;
  border-radius: 8px;
  border: 2px solid #00ff66;
}

.screen {
  min-height: 120px;
  border-bottom: 1px dashed #00ff66;
  margin-bottom: 20px;
}

.controls {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.middle-buttons {
  display: flex;
  gap: 20px;
}

button {
  background-color: #161b22;
  color: #00ff66;
  border: 1px solid #00ff66;
  padding: 10px 15px;
  font-family: inherit;
  cursor: pointer;
  transition: all 0.2s;
}

button:hover:not(:disabled) {
  background-color: #00ff66;
  color: #0d1117;
}

button:disabled {
  opacity: 0.3;
  cursor: not-allowed;
  border-color: #444;
  color: #888;
}
</style>