<template>
    <div>
        <div class="d-flex">
            <input class="form-control d-flex w-25" v-model="input" />
            <button class="btn btn-primary" @click="loadData()">szukaj</button>
        </div>
        <table class="table">
            <tr>
                <th>id</th>
                <th>name</th>
                <th>model</th>
            </tr>
            <tbody>
                <table-item
                    :user="this.user"
                    v-for="item in items"
                    :key="item.id"
                    :data="item"
                    @edit="editItem"
                    @delete="reloade"
                ></table-item>
            </tbody>
        </table>
        <the-form @reloade="reloade" v-if="rowId" :id="this.rowId"></the-form>
    </div>
</template>
<script>
import TableItem from "./TableItem.vue";
import theForm from "./form.vue";
export default {
    components: {
        theForm,
        TableItem,
    },
    data() {
        return {
            input: this.name,
            items: [],
            rowId: null,
        };
    },
    props: ["user"],
    methods: {
        loadData() {
            this.items = [];
            if (this.input == "" || this.input == undefined) {
                axios
                    .get("/api/items", {
                        headers: {
                            Authorization:
                                "Bearer " + localStorage.getItem("token"),
                        },
                    })
                    .then((respon) => {
                        this.items = respon.data;
                    })
                    .catch((err) => {
                        console.log(err);
                    });
            } else {
                axios
                    .get("https://laravelappnew.herokuapp.com/api/items/search/" + this.input, {
                        headers: {
                            Authorization:
                                "Bearer " + localStorage.getItem("token"),
                        },
                    })
                    .then((respon) => {
                        this.items = respon.data;
                    })
                    .catch((err) => {
                        console.log(err);
                    });
            }
        },
        editItem(data) {
            this.rowId = data;
        },
        reloade() {
            this.rowId = null;
            this.loadData();
        },
    },
    created() {
        this.loadData();
    },
};
</script>
