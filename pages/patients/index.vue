<template>
    <div>
        <v-app-bar color="white" elevation="1">
        </v-app-bar>
        <v-row class="ma-1">
            <v-col>
                <ui-patients />
            </v-col>
        </v-row>
    </div>
</template>
 
<script>
import uiPatientsVue from '~/components/uiPatients/uiPatients.vue'
export default {
    layout: 'dashboard',
    components: {
        uiPatientsVue
    }
}
</script>