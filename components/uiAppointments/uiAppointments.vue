<template>
    <v-card elevation="1">
        <v-card-title>

        </v-card-title>
        <v-card-text >
            <v-form ref="frmRegistro" v-model="frmRegistro" class="">
                <v-row align="center" justify="start" dense>
                    <v-col cols="7">
                        <v-text-field
                            class="ml-2"
                            type="text"
                            v-model="nombre"
                            placeholder="Buscar paciente"
                            rounded
                            filled
                            dense
                            height="43"
                        />
                    </v-col>
                    <v-tooltip right>
                            <template v-slot:activator="{ on, attrs }">
                            <v-btn
                                class="mx-3"
                                small
                                fab
                                outlined
                                color="green accent-3"
                                @click="registraUsuario"
                                v-bind="attrs"
                                v-on="on"
                            >
                                <v-icon color="black">mdi-plus</v-icon>
                            </v-btn>
                        </template>
                        <span>
                            Add new appointment
                        </span>
                    </v-tooltip>
                </v-row>
            </v-form>

            <v-data-table>

            </v-data-table>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    
}
</script>