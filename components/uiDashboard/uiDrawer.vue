<template>
    <v-navigation-drawer
        app
        permanent
        left
        width="250"
    >
        <v-list>
            <v-list-item>
              <v-img max-width="113px" max-height="45px" :src="require('/assets/images/descarga1.png')"></v-img>
            </v-list-item>
            <v-list-item >
                <v-list-item-avatar width="100px" height="100px" >
                    <v-img  :src="require('/assets/images/descarga.png')"></v-img>               
                </v-list-item-avatar>
            </v-list-item>
            <v-list-item-title class="text-body-1 text-center">
                My App
            </v-list-item-title>
        </v-list>
        <v-divider />
        <v-list nav dense>
            <v-list-item
                v-for="(item, i) in items"
                :key="i"
                link
            >
                <v-list-item-icon>
                    <v-icon>
                        {{ item.icon }}
                    </v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                    <v-list-item-title>
                        {{ item.title }}
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-list>
    </v-navigation-drawer>
</template>

<script>
export default {
    data () {
        return {
            items: [
                { title: 'Dashboard', icon: 'mdi-view-dashboard' },
                { title: 'Appointments', icon: 'mdi-book-clock' },
                { title: 'Patients', icon: 'mdi-account-multiple-plus' },
                { title: 'Schedule', icon: 'mdi-checkbox-marked-circle-outline'}
                ],
        }
    }
}
</script>

<style scoped>

</style>>