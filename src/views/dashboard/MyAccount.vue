<template>
    <div class="page-my-account">

        <h1 class="title">My account</h1>

        <div>
            <strong>Username: </strong>{{ $store.state.user.username }}
        </div>
        <div>
            <strong>My character: </strong>{{ character.name }}
        </div>
        <!-- <div>
            <img :src="character.image" class="responsive-image"/>
        </div> -->

        <hr>

        <div class="buttons">
            <router-link to="/dashboard/my-account/edit-character" class="btn btn-outline-primary me-2">Edit character</router-link>
            <button @click="logout()" class="btn btn-danger">Log out</button>
        </div>
    </div>
</template>

<style>
.responsive-image {
    width: 50vw; /* 50% of the viewport width */
    height: auto; /* Maintain aspect ratio */
}
</style>

<script>
import axios from 'axios'

export default {
    name: 'MyAccount',
    data() {
        return {
            character: {}
        }
    },
    async mounted() {
        await this.getOrCreateCharacter()
    },
    methods: {
        getOrCreateCharacter() {
            axios
                .get('/api/v1/character/')
                .then(response => {
                    this.character = response.data[0]
                    console.log(response.data)
                    console.log(this.character.id)
                    console.log(this.character.image)
                })
                .catch(error => {
                    console.log(JSON.stringify(error))
                })
        },
        logout() {
            axios
                .post("/api/v1/token/logout/")
                .then(response => {
                    axios.defaults.headers.common["Authorization"] = ""

                    localStorage.removeItem("username")
                    localStorage.removeItem("userid")
                    localStorage.removeItem("token")

                    this.$store.commit('removeToken')

                    this.$router.push('/')
                })
                .catch(error => {
                    if (error.response) {
                        console.log(JSON.stringify(error.response.data))
                    } else if (error.message) {
                        console.log(JSON.stringify(error.message))
                    } else {
                        console.log(JSON.stringify(error))
                    }
                })
        }
    }
}
</script>