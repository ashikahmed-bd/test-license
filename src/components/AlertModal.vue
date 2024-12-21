<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const alert = ref(false);
const message = ref('');

const verifyLicense = async () => {
  try {
    await axios.post('http://127.0.0.1:8000/api/license/verify', {
      license_key: 'LGLYU-ZN741-H1IR5-FO6TT-TTFTH',
      signature: 'd3shUwbLdUNtLW+ALOnZzl8E62dWEXCZ2SvNiv6LiddomzcdpjqfPpw8LZuQh0SsgKMOlPmaJaNrijgz6iGreEEGup1q+6e1sSu7nmEl86UYsNSr/nUdzw9MS+ZqmgQ0KS2zyRYM2xw8cftgIdn2xh+YNJVVzA+S6DuWjYqBgNtrIBXoIJESirbgZKsUCZdW36ChspACmJUsoJUfwsBqTBbeX6DB8w6e3xsIlKoTSgqLsTg7y1mT/mmamL+6HEa4GAZ2GNXET+XzvhFdAsMX/6BaZUuNU5AidWSyDRZFKr9zbgIBXYB/86QUzLkYNEVHtu0NqucOzzsB5W7BsiNoCw==',
    });
  } catch (error) {
    alert.value = true;
    message.value = error.response.data.message;
  }
};

onMounted(() => {
  verifyLicense();
});
</script>

<template>
  <div v-if="alert" class="modal-overlay">
    <div class="modal">
      <div class="modal-header">
        <div class="icon-container">
          ⚠️
        </div>
        <h2>Access Denied</h2>
      </div>
      <div class="modal-body">
        <p>{{message}}</p>
        <p><strong>Contact Information:</strong></p>
        <ul>
          <li>Email: <span>info@ashikahmed.net</span></li>
          <li>Phone: <span href="tel:data.phone">(880) 1911-742233</span></li>
          <li>Website: <span>www.ashikahmed.net</span></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
  width: 90%;
  max-width: 550px;
  padding: 30px;
  text-align: center;
  animation: fadeIn 0.3s ease-in-out;
}

.modal-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

.icon-container {
  font-size: 50px;
  color: #ff4d4d;
}

.modal-header h2 {
  font-size: 22px;
  color: #333;
  margin: 0;
}

.modal-body {
  font-size: 16px;
  color: #555;
  margin-bottom: 20px;
  line-height: 1.5;
}

.modal-body a {
  color: #007BFF;
  text-decoration: none;
}

.modal-body a:hover {
  text-decoration: underline;
}

.modal-body ul {
  list-style: none;
  padding: 0;
  margin: 10px 0 0;
}

.modal-body li {
  margin: 5px 0;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20%);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

</style>