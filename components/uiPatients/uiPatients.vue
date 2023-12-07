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
                                    small
                                    class="mx-3"
                                    outlined
                                    color="green accent-3"
                                    @click="registraPatient"
                                    v-bind="attrs"
                                    v-on="on"
                                    rounded
                                >
                                    Add new patient +
                                </v-btn>
                            </template>
                            <span>
                                Add new patient
                            </span>
                        </v-tooltip>
                    </v-row>
                </v-form>

                <v-data-table>

                </v-data-table>
            </v-card-text>

            <v-dialog
            v-model="dialog"
            max-width="749"
            max
            >
            <v-card height="850" width="749">
                <v-card-title class="text-h5">
                    Add new appointment
                </v-card-title>

                <v-card-text >
                    <form ref="frmRegistro" v-modal="frmRegistro">
                        <v-row>
                            <v-col>
                                Nombre
                            </v-col>
                            <v-col>
                                Apellido
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col>
                                <v-text-field 
                                    type="text"
                                    v-model="Nombre"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                            <v-col>
                                <v-text-field 
                                    type="text"
                                    v-model="Apellido"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col>
                                Email
                            </v-col>
                            <v-col>
                                Movile
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col>
                                <v-text-field 
                                    type="text"
                                    v-model="Email"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                            <v-col>
                                <v-text-field 
                                    type="text"
                                    v-model="Movile"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col cols="3">
                                Date of birth
                            </v-col>
                            <v-col cols="2">
                                Edad
                            </v-col>
                            <v-col>
                                Genero
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col cols="3">
                                <v-text-field 
                                    type="text"
                                    v-model="Birthday"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                            <v-col cols="2">
                                <v-text-field 
                                    type="text"
                                    v-model="Edad"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                            <v-col cols="7">
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
                            Address 
                        </v-row>
                        <v-row justify="start">
                            <v-text-field                                     type="text"
                                v-model="Cita"
                                :rules="[reglas.requerido]"
                                dense
                                rounded
                                solo
                                height="80"
                            />
                        </v-row>
                        <v-row>
                            <v-col>
                                Treatment
                            </v-col>
                            <v-col>
                                Blood group
                            </v-col>
                        </v-row>
                        <v-row>
                            <v-col>
                                <v-text-field 
                                    type="text"
                                    v-model="Tratmiento"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
                            <v-col>
                                <v-text-field 
                                    type="text"
                                    v-model="TipoSangre"
                                    :rules="[reglas.requerido]"
                                    dense
                                    rounded
                                    solo
                                />
                            </v-col>
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
                        Add patient
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