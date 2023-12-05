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
//import uiUsuariosVue from '~/components/uiUsers/uiUsuarios.vue'
export default {
    layout: 'dashboard',
    components: {
        uiAppointments,
        //uiUsuariosVue
    }
}
</script>