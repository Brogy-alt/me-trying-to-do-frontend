<template>
    <SpinnerComponent v-if="isSpinning" />
    
    <div class="container-fluid" v-else>
        <table class="table" >
            <thead>
                <tr>
                <th scope="col">ID</th>
                <th scope="col">First Name</th>
                <th scope="col">Last Name</th>
                <th scope="col">Gender</th>
                <th scope="col">cellphoneNumber</th>
                <th scope="col">Email Address</th>
                <th scope="col">Password</th>
                <th scope="col">Profile</th>
                <th scope="col">Date Joined</th>
                <th scope="col">Edit</th>
                <th scope="col">Delete</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user">
                <th scope="row">{{ user.userID }}</th>
                <td>{{ user.firstName }}</td>
                <td>{{ user.lastName }}</td>
                <td>{{ user.gender }}</td>
                <td>{{ user.cellphoneNumber }}</td>
                <td>{{ user.emailAdd }}</td>
                <td>{{ user.userPass }}</td>
                <td>{{ user.userRole }}</td>
                <td><img :src="user.userProfile" alt=""></td>
                <td>{{ user.joinDate }}</td>
                <td>Edit</td>
                <td>Delete</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
import { useStore } from 'vuex';
import { computed } from '@vue/runtime-core';
import SpinnerComponent from '@/components/SpinnerComponent.vue';

export default{
    components: {
        SpinnerComponent
    },

    setup() {
        const store = useStore()
        store.dispatch("fetchUsers")
        const users = computed(() => store.state.users)
        return{
            users
        }
    },
    created() {
        setTimeout(() => {
            this.isSpinning = false;
        }, 3000);
    },
    data() {
        return {
            isSpinning: true
        }
    }
}

</script>
<style scoped>
td {
    word-break: break-all;
    word-wrap: break-word;
}

img{
    height: 50px;
    width: 50px;
}
</style>