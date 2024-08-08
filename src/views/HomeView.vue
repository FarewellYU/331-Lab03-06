<template>
  <div class="passenger-list-container">
    <h1 class="title">Passenger List</h1>
    
    <div v-if="error" class="error-message">
      {{ error }}
    </div>
    
    <ul v-else class="passenger-list">
      <li v-for="passenger in passengers" :key="passenger._id" class="passenger-item">
        <router-link :to="{ name: 'PassengerDetail', params: { id: passenger._id } }" class="passenger-link">
          {{ passenger.name }}
        </router-link>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.passenger-list-container {
  padding: 2rem;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  max-width: 800px;
  margin: 0 auto;
}

.title {
  color: #007bff;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  text-align: center;
}

.error-message {
  color: #e74c3c;
  font-size: 1.2rem;
  text-align: center;
  margin-bottom: 1.5rem;
}

.passenger-list {
  list-style-type: none;
  padding: 0;
}

.passenger-item {
  margin-bottom: 1rem;
}

.passenger-link {
  display: block;
  padding: 1rem;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  text-decoration: none;
  color: #333;
  transition: background-color 0.3s, color 0.3s;
}

.passenger-link:hover {
  background-color: #007bff;
  color: #fff;
}
</style>
<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import { getPassengers } from '@/services/apiService';

export default defineComponent({
  name: 'HomeView',
  setup() {
    const passengers = ref<any[]>([]);
    const error = ref<string | null>(null);

    onMounted(async () => {
      try {
        const response = await getPassengers();
        passengers.value = response.data.data; // 处理分页数据，确保根据实际 API 响应结构进行调整
      } catch (err) {
        error.value = (err as Error).message;
        console.error("There was an error!", err);
      }
    });

    return { passengers, error };
  },
});
</script>

<style scoped>
.error {
  color: red;
  font-weight: bold;
}
</style>
