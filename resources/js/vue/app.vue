<template>
    <div class="p-2" v-if="user">
        <the-menu
            :user="this.user"
            @logout="logout"
            @add-data="seeForm"
        ></the-menu>
        <the-form v-if="this.addData"></the-form>
        <table-items :user="this.user" />
    </div>

    <Login v-else-if="reg" @register="register" @login="login"></Login>
    <register v-if="!reg" @register="register" @login="login"></register>
</template>
<script>
import theForm from "./components/form.vue";
import tableItems from "./components/TableItems.vue";
import theMenu from "./components/TheMenu.vue";
import Login from "./components/Login.vue";
import register from "./components/register.vue";
export default {
    components: {
        tableItems,
        theMenu,
        theForm,
        Login,
        register,
    },
    data() {
        return {
            id: null,
            addData: false,
            user: null,
            reg: true,
        };
    },
    methods: {
        register() {
            this.reg = !this.reg;
        },
        seeForm() {
            this.addData = !this.addData;
        },
        login(respon) {
            this.user = respon;
            // console.log(respon.user);
        },
        logout() {
            this.user = "";
            localStorage.removeItem("token");
            // console.log(this.user);
        },
    },
};
</script>
