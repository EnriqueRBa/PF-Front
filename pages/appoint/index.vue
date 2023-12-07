<template>
    <div>
        <v-app-bar color="white" elevation="1">
        </v-app-bar>
        <v-row class="ma-1">
            <v-col>
                <ui-appointments />
            </v-col>
        </v-row>
    </div>
</template>

<script>
import uiAppointments from '~/components/uiAppointments/uiAppointments.vue'
export default {
    layout: 'dashboard',
    components: {
        uiAppointments,
    },
    data() {
    return {
      appointments: [],
    };
  },
  mounted() {
    // Llamada a la API para obtener citas desde el backend
    this.fetchAppointments();
  },
  methods: {
    async fetchAppointments() {
      try {
        const response = await axios.get('http://localhost:3000/get-appointment');
        this.appointments = response.data;
      } catch (error) {
        console.error('Error al obtener citas:', error);
      }
    },
  },
}
</script>