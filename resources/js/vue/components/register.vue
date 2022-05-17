<template>
    <div>
        <label for
            >Name<input class="form-control" v-model="name" type="email"
        /></label>
        <label for
            >Email<input class="form-control" v-model="email" type="email"
        /></label>
        <label for
            >Password
            <input class="form-control" v-model="password" type="password"
        /></label>
        <label for
            >Password confirm
            <input
                class="form-control"
                v-model="password_confirmation"
                type="password"
        /></label>
        <button class="btn btn-primary" @click="sendData">rejestruj</button>
        <p>
            <button @click="$emit('register')">logowanie</button>
        </p>
    </div>
</template>
<script>
export default {
    data() {
        return {
            name: "",
            email: "",
            password: "",
            password_confirmation: "",
        };
    },
    methods: {
        sendData() {
            axios
                .post(
                    "https://laravelappnew.herokuapp.com/api/register",
                    {
                        name: this.name,
                        email: this.email,
                        password: this.password,
                        password_confirmation: this.password_confirmation,
                    },
                    {
                        headers: {
                            "Content-Type": "application/json",
                            Accept: "application/json",
                        },
                    }
                )
                .then(() => {
                    // const user = respon.data;
                    this.$emit("register");
                })
                .catch((err) => {
                    console.log(err);
                });
        },
    },
};
</script>
