<template>
    <form @submit.prevent="useData">
        <label for
            >nazwa <input class="form-control" v-model="name" type="text"
        /></label>
        <label for
            >model <input class="form-control" v-model="model" type="text"
        /></label>
        <input class="btn btn-primary" type="submit" />
    </form>
</template>

<script>
export default {
    props: ["id"],
    data() {
        return {
            name: "",
            model: "",
        };
    },
    methods: {
        useData() {
            if (this.id) {
                axios
                    .put(
                        "/api/item/" + this.id,
                        {
                            item: {
                                model: this.model,
                                name: this.name,
                            },
                        },
                        {
                            headers: {
                                Authorization:
                                    "Bearer " + localStorage.getItem("token"),
                            },
                        }
                    )
                    .then((respon) => {
                        this.items = respon.data;
                        this.$emit("reloade");
                    })
                    .catch((err) => {
                        console.log(err);
                    });
            } else {
                axios
                    .post(
                        "/api/item/store",
                        {
                            item: {
                                model: this.model,
                                name: this.name,
                            },
                        },
                        {
                            headers: {
                                Authorization:
                                    "Bearer " + localStorage.getItem("token"),
                            },
                        }
                    )
                    .then((respon) => {
                        this.items = respon.data;
                    })
                    .catch((err) => {
                        console.log(err);
                    });
            }
        },
    },
};
</script>
