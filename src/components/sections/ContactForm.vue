<template>
  <section id="contact" class="contact-section">
    <div class="container reveal">
      <h2>Ponte en <span class="gradient-text">contacto</span></h2>
      <div v-if="submitted" class="success-message">
        <h3>¡Mensaje enviado con éxito!</h3>
        <p>Gracias por contactarnos. Nuestro equipo de atención al cliente te responderá en un plazo de 24 horas.</p>
        <button @click="submitted = false" class="btn btn-primary" style="margin-top: 1rem">Enviar otro mensaje</button>
      </div>
      <form v-else class="contact-form" @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="name">Nombre Completo</label>
          <input
            type="text"
            id="name"
            v-model="formData.name"
            placeholder="Ej. Juan Pérez"
            :class="{ 'input-error': errors.name }"
          />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>
        
        <div class="form-group">
          <label for="email">Correo Electrónico</label>
          <input
            type="email"
            id="email"
            v-model="formData.email"
            placeholder="juan@ejemplo.com"
            :class="{ 'input-error': errors.email }"
          />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>

        <div class="form-group">
          <label for="subject">Asunto</label>
          <select 
            id="subject" 
            v-model="formData.subject"
            :class="{ 'input-error': errors.subject }"
          >
            <option value="">Selecciona un motivo</option>
            <option value="consulta">Consulta General</option>
            <option value="pedido">Estado de Pedido</option>
            <option value="devolucion">Devoluciones</option>
            <option value="mayorista">Venta al por Mayor</option>
          </select>
          <span v-if="errors.subject" class="error">{{ errors.subject }}</span>
        </div>

        <div class="form-group">
          <label for="message">Mensaje</label>
          <textarea
            id="message"
            v-model="formData.message"
            placeholder="Escribe tu mensaje aquí (mínimo 20 caracteres)..."
            :class="{ 'input-error': errors.message }"
          ></textarea>
          <span v-if="errors.message" class="error">{{ errors.message }}</span>
        </div>

        <div class="form-group checkbox-group">
          <label class="checkbox-container">
            <input type="checkbox" v-model="formData.privacy">
            <span class="checkmark"></span>
            Acepto la <a href="#">política de privacidad</a> y los términos de servicio.
          </label>
          <span v-if="errors.privacy" class="error">{{ errors.privacy }}</span>
        </div>

        <button type="submit" class="btn btn-primary" style="width: 100%">
          Enviar Mensaje
        </button>
      </form>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive, watch } from 'vue';

const formData = reactive({
  name: '',
  email: '',
  subject: '',
  message: '',
  privacy: false
});

const errors = reactive({
  name: '',
  email: '',
  subject: '',
  message: '',
  privacy: ''
});

const submitted = ref(false);

const validate = () => {
  let isValid = true;
  
  // Name validation
  if (!formData.name.trim()) {
    errors.name = 'El nombre es obligatorio';
    isValid = false;
  } else if (formData.name.trim().length < 3) {
    errors.name = 'El nombre debe tener al menos 3 caracteres';
    isValid = false;
  } else if (!/^[a-zA-ZáéíóúÁÉÍÓÚñÑ\s]+$/.test(formData.name)) {
    errors.name = 'El nombre solo puede contener letras';
    isValid = false;
  } else {
    errors.name = '';
  }

  // Email validation
  const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  if (!formData.email) {
    errors.email = 'El email es obligatorio';
    isValid = false;
  } else if (!emailRegex.test(formData.email)) {
    errors.email = 'El email no tiene un formato válido';
    isValid = false;
  } else {
    errors.email = '';
  }

  // Subject validation
  if (!formData.subject) {
    errors.subject = 'Debes seleccionar un asunto';
    isValid = false;
  } else {
    errors.subject = '';
  }

  // Message validation
  if (!formData.message.trim()) {
    errors.message = 'El mensaje es obligatorio';
    isValid = false;
  } else if (formData.message.trim().length < 20) {
    errors.message = 'El mensaje debe tener al menos 20 caracteres';
    isValid = false;
  } else {
    errors.message = '';
  }

  // Privacy validation
  if (!formData.privacy) {
    errors.privacy = 'Debes aceptar la política de privacidad';
    isValid = false;
  } else {
    errors.privacy = '';
  }

  return isValid;
};

const handleSubmit = () => {
  if (validate()) {
    console.log('Formulario enviado:', formData);
    // Simular envío
    submitted.value = true;
    // Reset form
    Object.keys(formData).forEach(key => {
      if (typeof formData[key] === 'boolean') formData[key] = false;
      else formData[key] = '';
    });
  }
};

// Real-time validation (optional but good for UX)
watch(() => formData.name, () => { if (errors.name) validate(); });
watch(() => formData.email, () => { if (errors.email) validate(); });
watch(() => formData.message, () => { if (errors.message) validate(); });
</script>

<style scoped>
.input-error {
  border-color: var(--error-color) !important;
}

select {
  width: 100%;
  padding: 0.875rem 1rem;
  background-color: #050505;
  border: 1px solid var(--border-color);
  border-radius: 12px;
  color: var(--white);
  font-family: inherit;
  font-size: 0.9375rem;
  transition: all 0.2s;
  cursor: pointer;
}

select:focus {
  outline: none;
  border-color: var(--primary-color);
}

.checkbox-group {
  margin-top: 1rem;
  text-align: left;
}

.checkbox-container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 0.875rem;
  color: var(--text-secondary);
  user-select: none;
}

.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #050505;
  border: 1px solid var(--border-color);
  border-radius: 4px;
}

.checkbox-container:hover input ~ .checkmark {
  border-color: var(--primary-color);
}

.checkbox-container input:checked ~ .checkmark {
  background-color: var(--primary-color);
  border-color: var(--primary-color);
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-container input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-container .checkmark:after {
  left: 7px;
  top: 3px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

.checkbox-container a {
  color: var(--primary-color);
  text-decoration: none;
}

.checkbox-container a:hover {
  text-decoration: underline;
}
</style>
