<template>
  <ion-page>
    <!-- Encabezado de la aplicación -->
    <ion-header :translucent="true">
      <ion-toolbar color="primary">
        <ion-title>Registro de Alumnos</ion-title>
      </ion-toolbar>
    </ion-header>

    <!-- Contenido principal con el formulario -->
    <ion-content :fullscreen="true" class="ion-padding">
      
      <div class="form-container">
        <h2 class="ion-text-center">Datos del Alumno</h2>

        <!-- Campo: Nombre -->
        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Nombre Completo" 
            label-placement="floating" 
            v-model="alumno.nombre"
            type="text">
          </ion-input>
        </ion-item>

        <!-- Campo: Matrícula -->
        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Matrícula" 
            label-placement="floating" 
            v-model="alumno.matricula"
            type="text">
          </ion-input>
        </ion-item>

        <!-- Campo: Correo -->
        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Correo Electrónico" 
            label-placement="floating" 
            v-model="alumno.correo"
            type="email">
          </ion-input>
        </ion-item>

        <!-- Campo: Carrera -->
        <ion-item fill="outline" mode="md" class="ion-margin-bottom">
          <ion-input 
            label="Carrera" 
            label-placement="floating" 
            v-model="alumno.carrera"
            type="text">
          </ion-input>
        </ion-item>

        <!-- Botones de Acción -->
        <div class="button-container ion-margin-top">
          <ion-button expand="block" color="success" @click="guardarAlumno">
            Guardar Alumno
          </ion-button>
          <ion-button expand="block" color="medium" fill="clear" @click="limpiarFormulario">
            Limpiar Campos
          </ion-button>
        </div>
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
  IonButton 
} from '@ionic/vue';

// Objeto reactivo para almacenar los campos del formulario
const alumno = ref({
  nombre: '',
  matricula: '',
  correo: '',
  carrera: ''
});

// Función para procesar y guardar la información
const guardarAlumno = () => {
  if (!alumno.value.nombre || !alumno.value.matricula) {
    alert('Por favor, llena al menos los campos de Nombre y Matrícula.');
    return;
  }
  
  console.log('Datos del alumno guardados con éxito:', alumno.value);
  alert(`Alumno ${alumno.value.nombre} registrado correctamente en la consola.`);
  limpiarFormulario();
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
.form-container {
  max-width: 500px;
  margin: 20px auto;
  padding: 15px;
  background: transparent;
}

h2 {
  font-weight: 600;
  margin-bottom: 25px;
  color: var(--ion-color-dark);
}

.button-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
