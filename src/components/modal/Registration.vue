<template>
  
    <div id="app">
    <v-app>
        <v-dialog v-model="dialog" max-width="600px" min-width="360px" transition="dialog-bottom-transition">
            <div>
                <v-tabs v-model="tab" show-arrows background-color="indigo darken-3" icons-and-text dark grow>
                    <v-tabs-slider color="blue lighten-3"></v-tabs-slider>
                    <v-tab v-for="i in tabs" :key="i">
                        <v-icon large>{{ i.icon }}</v-icon>
                        <div class="caption py-1">{{ i.name }}</div>
                    </v-tab>                     
                    <v-btn icon dark @click="dialog = false" >
                        <v-icon>mdi-close</v-icon>
                    </v-btn>                    
                    <v-tab-item>
                        <v-card class="px-4">
                            <v-card-text>
                                <v-form ref="loginForm" v-model="valid" lazy-validation>
                                    <v-row>
                                        <v-col cols="12">
                                            <v-text-field v-model="loginEmail" :rules="loginEmailRules" label="E-mail" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12">
                                            <v-text-field v-model="loginPassword" :append-icon="show1?'eye':'eye-off'" :rules="[rules.required, rules.min]" :type="show1 ? 'text' : 'password'" name="input-10-1" label="Password" hint="At least 8 characters" counter @click:append="show1 = !show1"></v-text-field>
                                        </v-col>
                                        <v-col class="d-flex" cols="12" sm="6" xsm="12">
                                        </v-col>
                                        <v-spacer></v-spacer>
                                        <v-col class="d-flex" cols="12" sm="3" xsm="12" align-end>
                                            <v-btn x-large block :disabled="!valid" color="success" @click="validopen = !validopen"> Login </v-btn>
                                            <v-bottom-sheet v-model="validopen">
                                                <v-sheet  class="text-center" height="200px" >
                                                    <v-btn  href="/" class="mt-6" text color="red"  @click="validopen = !validopen" >
                                                     close
                                                     </v-btn>
                                                     <div class="level-item has-text-centered">
                                                        <div>
                                                            <p class="title">Welcome back!</p>
                                                            <p class="heading">Now you are logged in</p>
                                                        </div>                                                    
                                                    </div>
                                                </v-sheet> 
                                            </v-bottom-sheet> 
                                        </v-col>
                                    </v-row>
                                </v-form>
                            </v-card-text>
                        </v-card>
                    </v-tab-item>
                    <v-tab-item>
                        <v-card class="px-4">
                            <v-card-text>
                                <v-form ref="registerForm" v-model="valid" lazy-validation>
                                    <v-row>
                                        <v-col cols="12" sm="6" md="6">
                                            <v-text-field v-model="firstName" :rules="[rules.required]" label="First Name" maxlength="20" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12" sm="6" md="6">
                                            <v-text-field v-model="lastName" :rules="[rules.required]" label="Last Name" maxlength="20" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12">
                                            <v-text-field v-model="email" :rules="emailRules" label="E-mail" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12" sm="6" md="6">
                                            <v-text-field v-model="phone" :rules="[rules.required]" label="Phone" maxlength="20" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12" sm="6" md="6">
                                            <v-text-field v-model="direction" :rules="[rules.required]" label="Direction" maxlength="20" required></v-text-field>
                                        </v-col>
                                        <v-col cols="12">
                                            <v-text-field v-model="password" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'" :rules="[rules.required, rules.min]" :type="show1 ? 'text' : 'password'" name="input-10-1" label="Password" hint="At least 8 characters" counter @click:append="show1 = !show1"></v-text-field>
                                        </v-col>
                                        
                                        <v-col cols="12">
                                            <v-text-field block v-model="verify" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'" :rules="[rules.required, passwordMatch]" :type="show1 ? 'text' : 'password'" name="input-10-1" label="Confirm Password" counter @click:append="show1 = !show1"></v-text-field>
                                        </v-col>
                                        <v-spacer></v-spacer>
                                        <v-col class="d-flex ml-auto" cols="12" sm="3" xsm="12">
                                            <v-btn x-large block :disabled="!valid" color="success" @click="validate">Register</v-btn>
                                        </v-col>
                                    </v-row>
                                </v-form>
                            </v-card-text>
                        </v-card>
                    </v-tab-item>
                </v-tabs>
            </div>
        </v-dialog>
    </v-app>
</div>
   
</template>
<script>
    export default {
        computed: {
            passwordMatch() {
                return () => this.password === this.verify || "Password must match";
            }
        },
        methods: {
            
            validate() {
                
                if (this.$refs.loginForm.validate()) {
                    // submit form to server/API here...
                }
            },
            
            reset() {
                this.$refs.form.reset();
            },
            resetValidation() {
                this.$refs.form.resetValidation();
             }
        },
        data: () => ({
        dialog: true,
        validopen:false,
        tab: 0,
        tabs: [
            {name:"Login", icon:"mdi-account"},
            {name:"Register", icon:"mdi-account-plus"}
                    ],
        valid: true,
    
        firstName: "",
        lastName: "",
        email: "",
        password: "",
        direction:"",
        phone:"",
        verify: "",
        loginPassword: "",
        loginEmail: "",
        loginEmailRules: [
        v => !!v || "Required",
        v => /.+@.+\..+/.test(v) || "E-mail must be valid"
        ],
        emailRules: [
        v => !!v || "Required",
        v => /.+@.+\..+/.test(v) || "E-mail must be valid"
        ],

        show1: false,
        rules: {
        required: value => !!value || "Required.",
        min: v => (v && v.length >= 8) || "Min 8 characters"
        }
  })
    }
</script>
