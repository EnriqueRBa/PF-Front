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
                                v-model="nombrebuscar"
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
                                    @click="registraPatient"
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

            <v-dialog
            v-model="dialog"
            max-width="530"
            max
            >
            <v-card height="750" width="527">
                <v-card-title class="text-h5">
                    Add new appointment
                </v-card-title>

                <v-card-text >
                    <form ref="frmRegistro" v-modal="frmRegistro">
                        <v-row>
                            Nombre
                        </v-row>
                        <v-row>
                            <v-text-field 
                                type="text"
                                v-model="Nombre"
                                :rules="[reglas.requerido]"
                                dense
                                rounded
                                solo
                            />
                        </v-row>
                        <v-row>
                            Email
                        </v-row>
                        <v-row>
                            <v-text-field 
                                type="text"
                                v-model="Email"
                                :rules="[reglas.requerido]"
                                dense
                                rounded
                                solo
                            />
                        </v-row>
                        <v-row>
                            Phone
                        </v-row>
                        <v-row>
                            <v-text-field 
                                type="phone"
                                v-model="Telefono"
                                :rules="[reglas.requerido]"
                                dense
                                rounded
                                solo
                            />
                        </v-row>
                        <v-row>
                            <v-col  sm="4">
                                Age
                            </v-col>
                            <v-col >
                                Gender
                            </v-col>
                        </v-row>
                        <v-row justify="space-around">
                            <v-col cols="3">
                                <v-text-field 
                                    type="text"
                                    v-model="Edad"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                    
                                />
                            </v-col>
                            <v-col cols="8">
                                <v-radio-group
                                    
                                    v-model="Genero"
                                    row
                                >
                                    <v-radio
                                        label="Male"
                                        value="1"
                                    />
                                    <v-radio 
                                        label="Female"
                                        value="2"
                                    />
                                    <v-radio 
                                        label="Other"
                                        value="3"
                                    />
                                </v-radio-group>
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col sm="5">
                                Date
                            </v-col>
                            <v-col >
                                Time
                            </v-col>
                        </v-row>
                        <v-row justify="start">
                            <v-col cols="5">
                                <v-text-field 
                                    type="text"
                                    v-model="Cita"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                            <v-col cols="5">
                                <v-text-field 
                                    type="text"
                                    v-model="Hora"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                        </v-row>
                        <v-row>
                            Book an appointment for
                        </v-row>
                        <v-row>
                            <v-radio-group
                                v-model="TipoCita"
                                row
                            >
                                <v-radio 
                                    label="Checkup"
                                    value="4"
                                />
                                <v-radio 
                                    label="Surgery"
                                    value="5"
                                />
                            </v-radio-group>
                        </v-row>
                    </form>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                        color="green accent-3"
                        rounded
                        block
                        depressed
                        @click="newPatient"
                    >
                        Add
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
        </v-card> 
        
    
</template>

<script>
export default {
    data () {
        return {
            column: null,
            row: null,
            dialog: false,
            frmRegistro: false,
            nombre: '',
            nombrebuscar: '',
            reglas: {
                requerido: value => !!value || 'Campo requerido',
                contraseña: value => value.length >= 8 || 'Minimo 8 caracteres'
            }
        }
    },
    methods: {
        registraPatient () {
            this.dialog = true
            this.nombre = ''
        },
        async newPatient () {
            this.frmRegistro = this.$refs.frmRegistro.validate()
            if(this.Genero === 1){
                this.Genero = 'male'
            }else if (this.gender === 2){
                this.Genero = 'female'
            }else{
                this.Genero = 'other'
            }

            if(this.TipoCita === 1){
                this.TipoCita = 'Checkup'
            }else if (this.para === 2){
                this.TipoCita = 'Surgery'
            }

            if(this.frmRegistro) {
                //
                const sendData = {
                    Nombre: this.Nombre,
                    Email: this.Email,
                    Telefomo: this.Telefono,
                    Edad: this.Edad,
                    Genero: this.Genero,
                    Cita: this.Cita,
                    Hora: this.Hora,
                    TipoCita: this.TipoCita
                }

                const rawResponse = await fetch('http://localhost:5000/new_appointment', {
                    method: 'POST',
                    headers: {
                        'Acceot': 'application/json',
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(sendData)
                });
                
                console.log('@@@ response => ', response)
            } else {

            }
        }
    }
}
</script>