<template>
    <v-card
        elevation="15"
        color="blue-grey darken-3"
        width="600"
    >
        <v-card-title class= "text-h4 green--text text--accent-3">
            LOGIN
        </v-card-title>
        <v-card-text>
            <v-form v-model="isValid" ref="formLogin">
                <v-row>
                    <v-text-field 
                        v-model="usuario"
                        color="cyan darken-1"
                        placeholder="Ingresa tu numero celular"
                        label="Numero celular"
                        clearable
                        outlined
                        filled
                        dense
                        rounded
                        counter
                        maxlength="10"
                        :rules="[regla.vacio, regla.minimo]"
                    />
                </v-row>
                <v-row>
                    <v-text-field 
                        v-model="password"
                        color="cyan darken-1"
                        placeholder="Ingresa tu contraseña"
                        label="Contraseña"
                        outlined
                        filled
                        dense
                        rounded
                        counter
                        :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                        :type="show1 ? 'text' : 'password'"
                        :rules="[regla.vacio, regla.contraseña]"
                        @click:append="show1 = !show1"
                    />
                </v-row>
                <v-row class="green--text text--accent-3">
                    Olvidó su contraseña?
                </v-row>
            </v-form>
        </v-card-text>
        <v-card-actions>
            <v-row class="pa-2 ma-2 " justify="space-around" align="center">
                <v-btn color="green accent-3" rounded block depressed @click="ingresarSistema">
                    Login
                </v-btn>
            </v-row>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            usuario: '',
            password: '',
            show1: false,
            isValid: false,
            regla: {
                vacio: value => !!value || 'Campo requerido',
                minimo: value => value.length > 9 || 'Deben ser 10 digitos',
                contraseña: value => value.length >= 8 || 'Minimo 8 caracteres'
            }
        }
    },
    methods: {
        ingresarSistema () {
            const valid = this.$refs.formLogin.validate()
            if (valid) {
                //codigo para cambiar de pagina
            } else {
                //mostrar alerta
                alert('Datos incorrectos')
            }
        }
    }
}
</script>