<template>
    <div class="page-edit-character">
        <nav class="breadcrumb" aria-label="breadcrumbs">
            <ul>
                <li><router-link to="/dashboard">Dashboard</router-link></li>
                <li><router-link to="/dashboard/my-account">My account</router-link></li>
                <li class="is-active"><router-link to="/dashboard/onboarding" aria-current="true">New Story</router-link></li>
            </ul>
        </nav>

        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Customize your story</h1>
            </div>

            <div class="column is-12">
                <div class="field">
                    <label>Setting: </label>
                    <select v-model="story.setting" required>
                        <option value="FO">Forest</option>
                        <option value="DE">Desert</option>
                        <option value="SP">Space</option>
                    </select>
                </div>
                
                <div class="field">
                    <label>Second Language: </label>
                    <select v-model="story.second_language">
                        <option value="ES">Spanish</option>
                        <option value="FR">French</option>
                        <option value="DE">German</option>
                        <option value="IT">Italian</option>
                        <option value="PT">Portuguese</option>
                        <option value="RU">Russian</option>
                        <option value="ZH">Chinese</option>
                        <option value="JA">Japanese</option>
                        <option value="AR">Arabic</option>
                        <option value="HI">Hindi</option>
                    </select>
                </div>

                <div class="field">
                    <div class="control">
                        <button class="button is-success" @click="submitForm">Create Story</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
    name: 'Onboarding',
    data() {
        return {
            story: {
                setting: 'FO',
                second_language: null,
                wordiness: 'MD'
            }
        }
    },
    methods: {
        submitForm() {
            toast({
                message: 'Generating story',
                type: 'is-info',
                // dismissible: true,
                // pauseOnHover: true,
                // duration: 2000,
                position: 'bottom-right',
            })
            axios
                .post(`/api/v1/story/`, this.story)
                .then(response => {
                    this.$router.push({
                        name: 'Story',
                        params: {id: response.data.id}
                    })
                })
                .catch(error => {
                    console.log(JSON.stringify(error))
                })
        }
    }
}
</script>