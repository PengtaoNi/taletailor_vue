<template>
    <div class="page-edit-character">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Edit character</h1>
            </div>

            <div class="column is-12">
                <div class="field">
                    <label>Name</label>
                    <div class="control">
                        <input type="text" class="input" v-model="character.name">
                    </div>
                </div>

                <!-- <div class="file">
                    <label class="file-label">
                        <input class="file-input" type="file" name="file">
                        <span class="file-cta">
                        <span class="file-icon">
                            <i class="fas fa-upload"></i>
                        </span>
                        <span class="file-label">
                            Choose a file…
                        </span>
                        </span>
                    </label>
                </div> -->

                <div class="field">
                    <div class="control">
                        <button class="btn btn-outline-primary me-2" @click="submitForm">Save</button>
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
    name: 'EditCharacter',
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
                    console.log(this.character.create_by)
                })
                .catch(error => {
                    console.log(JSON.stringify(error))
                })
        },
        submitForm() {
            const formData = new FormData();
            formData.append('name', this.character.name);

            const fileInput = document.querySelector('input[type="file"]');
            if (fileInput && fileInput.files[0]) {
                formData.append('image', fileInput.files[0]);
            }

            axios
                .patch(`/api/v1/character/${this.character.id}/`, formData, {
                    headers: {
                        'Content-Type': 'multipart/form-data'
                    }
                })
                .then(response => {
                    toast({
                        message: 'Character saved',
                        type: 'is-success',
                        dismissible: true,
                        pauseOnHover: true,
                        duration: 2000,
                        position: 'bottom-right',
                    })

                    this.$router.push('/dashboard/my-account')
                })
                .catch(error => {
                    console.log(JSON.stringify(error))
                })
        }
    }
}
</script>