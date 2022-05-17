<template>
    <tr>
        <td>{{ data.id }}</td>
        <td>{{ data.name }}</td>
        <td>{{ data.model }}</td>
        <td>
            <button
                v-if="this.user.admin"
                type="button"
                class="btn btn-primary"
                @click="$emit('edit', data.id)"
            >
                edytuj
            </button>
        </td>
        <td>
            <button
                v-if="this.user.admin"
                class="btn btn-danger"
                @click="deleteItem(data.id)"
            >
                usun
            </button>
        </td>
    </tr>
</template>

<script>
export default {
    props: ["user", "data"],
    methods: {
        deleteItem(id) {
            if (confirm("are you sure?")) {
                axios
                    .delete("/api/item/" + id, {
                        headers: {
                            Authorization:
                                "Bearer " + localStorage.getItem("token"),
                        },
                    })
                    .then((respon) => {
                        console.log(respon);
                        this.$emit("delete");
                    })
                    .catch((err) => {
                        console.log(err);
                    });
            }
        },
    },
};
</script>
