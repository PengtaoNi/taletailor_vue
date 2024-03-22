<template>
    <div class="page-edit-character">

        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">{{ story.title }}</h1>
            </div>
        </div>

        <div>
            <div v-for="(illustration, index) in story.illustrations" :key="illustration.id" class="scene">
                <img :src="illustration.image" alt="Illustration" class="illustration-image"/>
                <div class="scene-text">{{ getSceneText(index) }}</div>
                <hr>
            </div>
        </div>

        <!-- <div class="column is-12">
            <div class="content">
                <p>{{ story.text }}</p>
            </div>
        </div>

        <div v-for="illustration in story.illustrations" :key="illustration.id">
            <img :src="illustration.image" alt="Illustration" />
        </div> -->
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
        getSceneText(index) {
            const scenes = this.story.text.split('\n');
            return scenes[index];
        },
    }
}
</script>