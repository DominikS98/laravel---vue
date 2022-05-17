<template>
    <div>
        <label for
            >Email<input class="form-control" v-model="email" type="email"
        /></label>
        <label for
            >password
            <input class="form-control" v-model="password" type="password"
        /></label>
        <button class="btn btn-primary" @click="sendData">zaloguj</button>
        <p>
            nie masz konta?
            <button @click="$emit('register')">rejestracja</button>
        </p>
    </div>
</template>
<script>
export default {
    data() {
        return {
            email: "",
            password: "",
        };
    },
    methods: {
        sendData() {
            axios
                .post(
                    "/api/login",
                    {
                        email: this.email,
                        password: this.password,
                    },
                    {
                        headers: {
                            "Content-Type": "application/json",
                            Accept: "application/json",
                        },
                    }
                )
                .then((respon) => {
                    const user = respon.data;
                    console.log(user);
                    localStorage.setItem("token", user.token);
                    this.$emit("login", user);
                })
                .catch((err) => {
                    console.log(err);
                });
        },
    },
};
</script>
