<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <v-card class="elevation-12">
              <v-window v-model="step">
                <v-window-item :value="1">
                  <v-row>
                    <v-col cols="12" md="8">
                        <v-card-text class="mt-12">
                            <h4 class="text-center mt-4">Login</h4>
                            <v-form>
                                <v-text-field
                                label="correo"
                                name="Email"
                                type="text"
                                color="teal accent-3"
                                v-model="emailLogin"
                                :rules="[v => !!v || 'El email es requerido',
                                v => /.+@.+/.test(v) || 'E-mail debe de ser valido',
                                ]"
                                />
                            <v-text-field
                            id="password"
                            label="Password"
                            name="password"
                            type="password"
                            color="teal accent-3"
                            v-model="passwordLogin"
                            :rules="[v => !!v || 'La contraseña es requerida']"
                          />
                        </v-form>
                        <h5
                          class="text-center"
                          
                        >{{this.mensajesrecovery}}</h5>
                        <h3 class="text-center mt-4">Olvidaste tu contraseña?</h3>
                        <div class="text-center mt-3">
                            <v-btn rounded color="teal accent-3" dark @click="step--">Recuperar password</v-btn>
                            
                        </div>
                      </v-card-text>
                      <div class="text-center mt-3">
                        <v-btn rounded color="teal accent-3"  @click="Login()" dark>Iniciar sesion</v-btn>
                      </div>
                    </v-col>
                    <v-col cols="12" md="4" class="teal accent-3">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Bienvenido</h1>
                        <h5
                          class="text-center"
                        >Ingresa ya para poder dara tus servicios a las personas</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn rounded outlined dark @click="step++">Registrate</v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="2">
                  <v-row class="fill-height">
                    <v-col cols="12" md="4" class="teal accent-3">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Bienvenido</h1>
                        <h5
                          class="text-center"
                        >Mantente conectado con tus clientes para poder generar mas ingresos haciendo lo que te gusta</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn rounded outlined dark @click="step--">Iniciar sesion</v-btn>
                      </div>
                    </v-col>

                    <v-col cols="12" md="8">
                      <v-card-text class="mt-12">
                        <h1 class="text-center display-2 teal--text text--accent-3">Crea una cuenta</h1>
                        <h4 class="text-center mt-4">Asegure su correo para registrarse</h4>
                        <v-form v-model='isValid'>
                          <v-text-field
                            label="Nombre"
                            name="Name"
                            type="text"
                            color="teal accent-3"
                            v-model='userRegister.firstname'
                            :rules="[v => !!v || 'El nombre es requerida',
                            v => (v && v.length >= 3) || 'El nombre debe contener mas de 3 caracteres']"
                            
                          />
                          <v-text-field
                            label="Apellido Paterno"
                            name="Name"
                            type="text"
                            color="teal accent-3"
                            v-model='userRegister.lastname'
                            :rules="[v => !!v || 'El apillodo paterno es requerida',
                            v => (v && v.length >= 3) || 'El nombre debe contener mas de 3 caracteres']"
                          />
                          <v-text-field
                            label="Apellido Materno"
                            name="Name"
                            type="text"
                            color="teal accent-3"
                            v-model="userRegister.secondname"
                            :rules="[v => !!v || 'El apellido materno es requerida',
                            v => (v && v.length >= 3) || 'El nombre debe contener mas de 3 caracteres']"
                          />
                          <v-select
                          :items="dataSelectSexo"
                          item-text="strCampo"
                          item-value="strCampo"
                          label="Sexo"
                          v-model="userRegister.Sex"
                          :rules="[v => !!v || 'El sexo es requerido']"
                          />
                          <v-text-field
                            label="Email"
                            name="Email"
                            type="text"
                            color="teal accent-3"
                            v-model="userRegister.email"
                            :rules="[v => !!v || 'El email es requerido',
                            v => /.+@.+/.test(v) || 'E-mail debe de ser valido',
                            ]"
                          />
                          <v-text-field
                            id="password"
                            label="Password"
                            name="password"
                            type="password"
                            color="teal accent-3"
                            v-model="userRegister.password"
                            :rules="[v => !!v || 'La contraseña es requerida',
                            v => (v && v.length >= 8) || 'El password debe contener mas de 8 caracteres',
                            v => /(?=.*[A-Z])/.test(v) || 'Debe contener almenos una Mayuscula',
                            v => /(?=.*\d)/.test(v) || 'Debe tener un numero',
                            v => /([!@$%])/.test(v) || 'Debe tener un carácter especial [!@#$%]']"
                            required
                          />
                          <div class="text-center mt-n5">
                            <v-btn rounded color="teal accent-3" :disabled="!isValid" @click="Registration()" dark>Registrar</v-btn>
                          </div>
                        </v-form>
                      </v-card-text>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="0">
                  <v-row class="fill-height">
                    <v-col cols="12" md="4" class="teal accent-3">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Cuidado, no compartir email</h1>
                        <h5
                          class="text-center"
                        >Mantente conectado con tus clientes para poder generar mas ingresos haciendo lo que te gusta</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn rounded outlined dark @click="step++">Volver a registro</v-btn>
                      </div>
                    </v-col>

                    <v-col cols="12" md="8">
                      <v-card-text class="mt-12">
                        <v-form>
                          <v-text-field
                            label="Email"
                            name="Email"
                            type="text"
                            color="teal accent-3"
                            v-model="emailRecovery" 
                            :rules="[v => !!v || 'El email es requerido',
                            v => /.+@.+/.test(v) || 'E-mail debe de ser valido',
                            ]"
                          />
                          
                        </v-form>
                      </v-card-text>
                      <div class="text-center mt-n5">
                        <v-btn rounded color="teal accent-3" @click="Recovery()" dark>Recuperar</v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import * as crypto from 'crypto';
import axios from "axios";

export default {
  data: () => ({
    step: 1,
    isValid: true,
    emailRecovery:'',
    emailLogin:'',
    mensajesrecovery : "",
    passwordLogin:'',
    userRegister:{
        firstname: "",
        lastname: "",
        secondname: "",
        Sex: "",
        email: "",
        password: "",
        token: "",
        catRolId: 2,
    },
    dataSelectSexo:
    [
      {id:1,strCampo:"Hombre"},
      {id:2,strCampo:"Mujer"}
    ],
  }),
  props: {
    source: String
  },
  methods: {
    Registration() {
      
      const cript = this.userRegister.email;
      const crypotopass = crypto.createHash('sha256').update(cript).digest('hex');
      this.userRegister.token = crypotopass;
      axios.post(`https://apipet18301044.herokuapp.com/users/`,this.userRegister).then(() => {
      this.step=1;
      this.mensajesrecovery= `Se creo correctamente el usuario`;
      })
    },
    Login() {
      axios.get("https://apipet18301044.herokuapp.com/login/"+this.emailLogin+"/"+this.passwordLogin).then((result) => {
      this.result = result.data;
      
      })
    },
    Recovery() {
      axios.get("https://apipet18301044.herokuapp.com/recuperarPassword/"+this.emailRecovery).then((result) => {
      this.result = result.data;
      this.step=1;
      this.mensajesrecovery= this.result.mensaje;
      })
    },
  },
  
};
</script>