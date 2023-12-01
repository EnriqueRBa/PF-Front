<template>
    <v-app>
        <ui-drawer-vue />
        <v-main>
        <Nuxt />
        </v-main>
    </v-app>
</template>

<script>
    import uiDrawerVue from '~/components/uiDashboard/uiDrawer.vue'
    
    export default {
        components: {
            uiDrawerVue
        },
        data () {
            return {

            }
        },
    }
</script>