<template>
  <div class="passenger-detail">
    <h1>Passenger Detail</h1>
    <div v-if="passenger">
      <p><strong>Name:</strong> {{ passenger.name }}</p>
      <p><strong>Trips:</strong> {{ passenger.trips }}</p>
      
      <div v-if="airline" class="airline-detail">
        <h2>Airline Details</h2>
        <p><strong>Name:</strong> {{ airline.name }}</p>
        <p><strong>Country:</strong> {{ airline.country }}</p>
        <img :src="airline.logo" alt="Airline Logo" v-if="airline.logo" class="airline-logo"/>
      </div>
      
      <router-view />
    </div>
    <div v-else class="loading">
      <p>Loading or no data available...</p>
    </div>
  </div>
</template>

<style scoped>
.passenger-detail {
  padding: 1.5rem;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  margin: 0 auto;
}

.passenger-detail h1 {
  color: #333;
  font-size: 2rem;
  margin-bottom: 1rem;
}

.passenger-detail p {
  color: #555;
  margin-bottom: 0.5rem;
}

.airline-detail {
  margin-top: 2rem;
  padding: 1rem;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.airline-detail h2 {
  margin-bottom: 0.75rem;
  color: #007bff;
}

.airline-logo {
  margin-top: 1rem;
  max-width: 100px;
  border-radius: 4px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

.loading {
  text-align: center;
  color: #999;
  font-size: 1.2rem;
}
</style>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { getPassengerById, getAirlineById } from '@/services/apiService';

export default defineComponent({
  name: 'PassengerDetailView',
  setup() {
    const route = useRoute();
    const router = useRouter();
    const passenger = ref<any>(null);
    const airline = ref<any>(null);

    onMounted(async () => {
      const passengerId = route.params.id as string;

      try {
        const passengerResponse = await getPassengerById(passengerId);
        passenger.value = passengerResponse.data;

        if (passenger.value.airline.length > 0) {
          const airlineId = passenger.value.airline[0]._id;
          const airlineResponse = await getAirlineById(airlineId);
          airline.value = airlineResponse.data;
        }
      } catch (error) {
        console.error("There was an error!", error);
        router.push({ name: 'NotFound' });
      }
    });

    return { passenger, airline };
  },
});
</script>
