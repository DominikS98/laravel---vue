<template>
    <div class="p-0 bg-light text-white">
        <button
            v-if="this.user.admin"
            class="btn btn-primary m-3"
            @click="$emit('addData')"
        >
            dodaj
        </button>
        <button class="btn btn-primary" @click="logout">wyloguj</button>
    </div>
</template>

<script>
export default {
    props: ["user"],
    methods: {
        logout() {
            axios
                .post("https://laravelappnew.herokuapp.com/api/logout", {
                    headers: {
                        Authorization:
                            "Bearer " + localStorage.getItem("token"),
                    },
                })
                .then(() => {
                    this.$emit("logout");
                })
                .catch((err) => {
                    console.log(err);
                });
        },
    },
};
</script>
