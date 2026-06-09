<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="primary">
        <ion-title>Registro de Alumnos</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      
      <div class="form-container">
        <h2 class="ion-text-center">Datos del Alumno</h2>

        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Nombre Completo" 
            label-placement="floating" 
            v-model="alumno.nombre"
            type="text">
          </ion-input>
        </ion-item>

        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Matrícula" 
            label-placement="floating" 
            v-model="alumno.matricula"
            type="text">
          </ion-input>
        </ion-item>

        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Correo Electrónico" 
            label-placement="floating" 
            v-model="alumno.correo"
            type="email">
          </ion-input>
        </ion-item>

        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Carrera" 
            label-placement="floating" 
            v-model="alumno.carrera"
            type="text">
          </ion-input>
        </ion-item>

        <div class="button-container ion-margin-top">
          <ion-button expand="block" color="success" @click="guardarAlumno">
            Guardar Alumno
          </ion-button>
          <ion-button expand="block" color="medium" fill="clear" @click="limpiarFormulario">
            Limpiar Campos
          </ion-button>
        </div>
      </div>

      <div class="lista-container ion-margin-top">
        <h3 class="ion-text-center section-title">Alumnos Registrados ({{ listaAlumnos.length }})</h3>
        
        <p v-if="listaAlumnos.length === 0" class="ion-text-center no-data">
          No hay alumnos registrados todavía.
        </p>

        <ion-card v-for="(item, index) in listaAlumnos" :key="index" class="student-card">
          <ion-item lines="none">
            <ion-label>
              <h2 class="student-name">{{ item.nombre }}</h2>
              <p><strong>Matrícula:</strong> {{ item.matricula }}</p>
              <p v-if="item.correo"><strong>Correo:</strong> {{ item.correo }}</p>
              <p v-if="item.carrera"><strong>Carrera:</strong> {{ item.carrera }}</p>
            </ion-label>
            
            <ion-button slot="end" fill="clear" color="danger" @click="eliminarAlumno(index)">
              <ion-icon :icon="trashOutline"></ion-icon>
            </ion-button>
          </ion-item>
        </ion-card>
      </div>

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { 
  IonContent, 
  IonHeader, 
  IonPage, 
  IonTitle, 
  IonToolbar, 
  IonItem, 
  IonInput, 
  IonButton,
  IonLabel,
  IonCard,
  IonIcon // Importamos el componente de iconos
} from '@ionic/vue';
import { trashOutline } from 'ionicons/icons'; // Importamos el icono de basura específico

// Estructura de un alumno
interface Alumno {
  nombre: string;
  matricula: string;
  correo: string;
  carrera: string;
}

// Objeto reactivo para capturar los campos del formulario
const alumno = ref<Alumno>({
  nombre: '',
  matricula: '',
  correo: '',
  carrera: ''
});

// Arreglo reactivo para guardar la lista de alumnos temporalmente
const listaAlumnos = ref<Alumno[]>([]);

// Función para añadir el alumno a la lista
const guardarAlumno = () => {
  if (!alumno.value.nombre || !alumno.value.matricula) {
    alert('Por favor, llena al menos los campos de Nombre y Matrícula.');
    return;
  }
  
  listaAlumnos.value.push({ ...alumno.value });
  limpiarFormulario();
};

// NUEVO: Función para eliminar un alumno específico por su posición (index)
const eliminarAlumno = (index: number) => {
  const nombreAlumno = listaAlumnos.value[index].nombre;
  if (confirm(`¿Estás seguro de que deseas eliminar a ${nombreAlumno}?`)) {
    listaAlumnos.value.splice(index, 1);
  }
};

// Función para reiniciar los valores del formulario
const limpiarFormulario = () => {
  alumno.value = {
    nombre: '',
    matricula: '',
    correo: '',
    carrera: ''
  };
};
</script>

<style scoped>
.form-container, .lista-container {
  max-width: 500px;
  margin: 20px auto;
  padding: 15px;
}

h2 {
  font-weight: 600;
  margin-bottom: 25px;
  color: var(--ion-color-dark);
}

.section-title {
  font-weight: 600;
  color: var(--ion-color-dark);
  border-top: 1px solid var(--ion-color-step-200);
  padding-top: 20px;
  margin-top: 30px;
}

.no-data {
  color: var(--ion-color-step-600);
  font-style: italic;
  margin-top: 15px;
}

.student-card {
  margin: 10px 0;
  border-left: 5px solid var(--ion-color-primary);
}

.student-name {
  font-size: 1.1rem !important;
  font-weight: bold !important;
  color: var(--ion-color-primary) !important;
  margin-bottom: 5px;
}

.button-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

/* Estilo para que el icono se vea un poco más grande y estético */
ion-icon {
  font-size: 1.4rem;
}
</style>