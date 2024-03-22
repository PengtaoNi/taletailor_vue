<template>
    <div class="page-edit-character">

        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">{{ story.title }}</h1>
            </div>
        </div>

        <div class="column is-12">
            <div class="content">
                <p>{{ story.text }}</p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
    name: 'Story',
    data() {
        return {
            story: {}
        }
    },
    mounted() {
        this.getStory()
    },
    methods: {
        getStory() {
            const story_id = this.$route.params.id

            axios
                .get(`/api/v1/story/${story_id}`)
                .then(response => {
                    this.story = response.data
                })
                .catch(error => {
                    console.log(JSON.stringify(error))
                })
        },
    }
}
</script>