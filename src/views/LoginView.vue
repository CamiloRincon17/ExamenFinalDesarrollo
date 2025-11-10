<template>
  <div class="split-screen-container">
    <!-- Left Pane (Image) - Hidden on small screens -->
    <div class="left-pane d-none d-md-block"></div>

    <!-- Right Pane (Form) -->
    <div class="right-pane d-flex align-items-center justify-content-center">
      <div class="form-wrapper">
        <h2 class="fw-bold mb-3 text-white">¡Qué alegría verte de nuevo!</h2>
        <h4 class="mb-4 text-white">Entrar</h4>

        <div v-if="alert.message" :class="`alert alert-${alert.type}`" role="alert">
          {{ alert.message }}
        </div>

        <form @submit.prevent="login">
          <div class="mb-3">
            <label for="username" class="form-label text-white">Tu correo</label>
            <input
              v-model="username"
              type="text"
              class="form-control bg-dark text-white border-0"
              id="username"
              placeholder="correo@ejemplo.com"
              required
            />
          </div>

          <div class="mb-3">
            <label for="password" class="form-label text-white">Tu contraseña</label>
            <div class="input-group">
              <input
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                class="form-control bg-dark text-white border-0"
                id="password"
                placeholder="••••••••"
                required
              />
              <button
                class="btn btn-outline-secondary"
                type="button"
                @click="togglePassword"
              >
                👁
              </button>
            </div>
          </div>

          <div class="mb-3 text-end">
            <a href="#" class="text-success text-decoration-none">¿Olvidaste la contraseña?</a>
          </div>

          <button type="submit" class="btn btn-custom w-100 mb-3">ENTRAR</button>

          <p class="text-center text-white">
            ¿No tienes cuenta? <a href="#" class="text-success">Crear cuenta</a>
          </p>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import usuarios from '../data/usuarios.json' // archivo local con usuarios

const username = ref('')
const password = ref('')
const showPassword = ref(false)
const router = useRouter()

const alert = ref({ message: '', type: 'danger' })

const togglePassword = () => {
  showPassword.value = !showPassword.value
}

const login = () => {
  if (!username.value || !password.value) {
    alert.value = { message: 'Por favor ingresa usuario y contraseña', type: 'warning' }
    setTimeout(() => { alert.value = { message: '', type: 'danger' } }, 3000)
    return
  }

  const user = usuarios.find(u => u.username === username.value && u.password === password.value)

  if (user) {
    // Guardar sesión básica
    localStorage.setItem('isAuthenticated', 'true')
    localStorage.setItem('userRole', user.role || 'user')
    localStorage.setItem('username', user.username)

    // Redirigir según rol
    if (user.role === 'admin') {
      router.push('/dashboard')
    } else {
      router.push('/productos')
    }
  } else {
    alert.value = { message: 'Credenciales inválidas', type: 'danger' }
    // limpiar alerta luego de 3s
    setTimeout(() => { alert.value = { message: '', type: 'danger' } }, 3000)
  }
}
</script>

<style scoped>
.split-screen-container {
  display: flex;
  min-height: 100vh;
  width: 100%;
  background-color: #121218; /* Fallback for the form side */
}

.left-pane {
  flex: 1;
  background-image: url("https://cloudfront-us-east-1.images.arcpublishing.com/grupoclarin/QNUQ5DOKIVG7JLNGJJFJNAQLSM.jpg");
  background-size: cover;
  background-position: center;
}

.right-pane {
  flex: 1;
  padding: 3rem;
  background-color: #121218;
}

.form-wrapper {
  max-width: 450px;
  width: 100%;
}

.btn-custom {
  background-color: #00ff90;
  color: #000;
  font-weight: bold;
  transition: 0.3s;
  border: none;
}

.btn-custom:hover {
  background-color: #00cc72;
  color: #000;
}

.btn-outline-secondary {
  border-color: #6c757d;
  color: #6c757d;
  background-color: transparent;
}

.btn-outline-secondary:hover {
  background-color: #6c757d;
  border-color: #6c757d;
  color: #fff;
}

.form-control.bg-dark {
  background-color: #1a1a1a !important;
  color: #fff !important;
}

.form-control.bg-dark:focus {
  background-color: #1a1a1a;
  color: #fff;
  border-color: #00ff90;
  box-shadow: 0 0 0 0.2rem rgba(0, 255, 144, 0.25);
}

.alert {
  margin-bottom: 1rem;
}

/* On smaller screens, the right pane takes the full width */
@media (max-width: 767.98px) {
  .right-pane {
    width: 100%;
    padding: 2rem 1.5rem;
  }
  
  .form-wrapper {
    max-width: 100%;
  }
}
</style>
