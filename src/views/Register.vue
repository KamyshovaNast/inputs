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
            this.axios.get('http://37.77.104.246/api/jsonstorage/?id=f552f48bfc2a4b25313ec74295dce42d')
                .then (
                    (response) => {
                        let users = response.data;
                        let user = {
                            login: this.login,
                            password: this.password
                        };
                        users.push(user);
                        this.axios.put('http://37.77.104.246/api/jsonstorage/?id=f552f48bfc2a4b25313ec74295dce42d', users);
                        this.$router.push('home')
                    }
                )
        }
    }
}
</script>
