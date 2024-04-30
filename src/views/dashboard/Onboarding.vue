<template>
  <div class="container mt-4">
    <div class="row justify-content-center">
      <div class="col-md-8" style="font-family: mali;">
        <h1 class="mb-4 text-center">Customize your story</h1>

        <form @submit.prevent="submitForm">
          <div class="py-2 form-group">
            <label for="setting">Setting:</label>
            <select id="setting" class="form-control" v-model="story.setting" required>
              <option value="FO">Forest</option>
              <option value="DE">Desert</option>
              <option value="SP">Space</option>
            </select>
          </div>

          <div class="py-2 form-group">
            <label for="second_language">Second Language:</label>
            <select id="second_language" class="form-control" v-model="story.second_language" required>
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

          <div class="py-2 form-group">
            <button type="submit" class="btn btn-success">Create Story</button>
          </div>
        </form>
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
        setting: null,
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