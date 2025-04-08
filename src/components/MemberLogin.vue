<template> 
    <v-container>
        <v-row justify="center">
            <v-col md="4">
                <v-card>
                    <v-card-title class="text-h5 text-center">  
                        로그인
                    </v-card-title>
                    <v-card-text>
                        <v-form>
                            <v-text-field
                                label="email"
                                v-model="email"
                            >
                            </v-text-field>
                            <v-text-field
                                label="패스워드"
                                v-model="password"
                                type="password"
                            >
                            </v-text-field>
                            <v-btn type="button" color="primary" block @Click="memberLogin()">로그인</v-btn>
                        </v-form>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import axios from 'axios';

    export default{
        data(){
            return{
                email : "",
                password : ""
            }
        },
        methods:{
            async memberLogin(){
                const loginData = {
                    email: this.email,
                    password: this.password
                }
                const response = await axios.post("http://localhost:8080/member/doLogin", loginData);
                const token = response.data.token; // 이름이 token인 것을 꺼냄 cf)아이디 꺼내고 싶으면 .id;
                localStorage.setItem("token", token); // 헤더컴포넌트에서, localStorage에 "token" 있으면 로그인(o) 처리했었음.
                window.location.href ="/";
            }
        }
    }
 </script>