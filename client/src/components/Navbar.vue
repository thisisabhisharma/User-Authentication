<template>
    <nav class="navbar navbar-expend-lg navbar-dark bg-dark">
        <button class="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#navbar1"
            aria-controls="navbar1"
            aria-expanded="false"
            aria-label="Toggle navigation"
        >
        <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse justify-content-md-center" id="navbar1">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <router-link class="nav-link" to="/">Welcome</router-link>
                </li>
                <li class="nav-item">
                    <router-link class="nav-link" to="/home">Home</router-link>
                </li>

                <li v-if="auth=='' && (token==null || token==undefined)" class="nav-item">
                    <router-link class="nav-link" to="/login">Login</router-link>
                </li>
                <li v-if="auth=='' && (token==null || token==undefined) " class="nav-item">
                    <router-link class="nav-link" to="/register">Register</router-link>
                </li>
                <li v-if="auth=='loggedin' || token!=null || token!=undefined" class="nav-item">
                    <router-link class="nav-link" to="/profile">Profile</router-link>
                </li>
                <li v-if="auth=='loggedin' || token!=null || token!=undefined" class="nav-item">
                    <a class="nav-link" href="" v-on:click="logout">Logout</a>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script>
import EventBus from './EventBus'

export default {
    data() {
        return {
            auth: '',
            token: localStorage.userToken
        }
    },
    methods: {
        logout() {
            localStorage.removeItem('userToken')
        } 
    },
    mounted() {
        EventBus.$on('logged-in', status => {
            this.auth = status
        })
    }
}
</script>