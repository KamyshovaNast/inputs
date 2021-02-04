<template>
    <div class="d-flex justify-center">
       <h1>Регистрация</h1>
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Регистрация аккаунта
            </v-card-title>

            <v-text-field
                label="Введите логин"
                v-model="login"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите пароль"
                v-model="password"
                outlined
            ></v-text-field>

            <v-btn @click="authenticate">
                Зарегистрироваться
            </v-btn>
        </v-card>
    </div>
</template>

<script>
// @ is an alias to /src
export default {
    data() {
        return {
            login: undefined,
            password: undefined,
            storage: ''
        }
    },
    methods: {
        authenticate() {
            this.axios.get('http://188.225.47.187/api/jsonstorage/d3cec8d60e3625b856a50c0722f2c8ab')
                .then (
                    (response) => {
                        let users = response.data;
                        let user = {
                            login: this.login,
                            password: this.password
                        };
                        users = users.push(user);
                        this.axios.put('http://188.225.47.187/api/jsonstorage/d3cec8d60e3625b856a50c0722f2c8ab', users);
                        this.$router.push('home')
                    }
                )
        }
    }
}
</script>
