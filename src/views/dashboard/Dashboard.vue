<template>
  <div class="page-dashboard">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="column is-12 has-text-centered py-3" style="font-family: mali-bold; text-align: center; color: #2b2f97;">My Stories</h1>
      </div>
    </div>
    <div class="column is-12">
      <div class="row">
        <div class="col-md-2" v-for="story in stories" :key="story.id">
          <router-link :to="`/dashboard/story/${story.id}`" class="card mb-4 shadow-sm">
            <img :src="story.illustrations[0].image" class="card-img-top" alt="Story cover">
            <div class="card-body">
              <p class="card-text" style="font-family: mali-bold; font-size: 24px;">{{ story.title }}</p>
              <p class="card-text" style="font-size: 16px;">Second Language: {{ LANGUAGE_CHOICES[story.second_language] }}</p>
              <div class="d-flex justify-content-between align-items-center">
                <!-- <div class="btn-group">
                  <button type="button" class="btn btn-sm btn-outline-secondary">View</button>
                  <button type="button" class="btn btn-sm btn-outline-secondary">Edit</button>
                </div> -->
              </div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Dashboard',
  data() {
    return {
      stories: [],
      LANGUAGE_CHOICES: {
        'ES': 'Spanish',
        'FR': 'French',
        'DE': 'German',
        'IT': 'Italian',
        'PT': 'Portuguese',
        'RU': 'Russian',
        'ZH': 'Chinese',
        'JA': 'Japanese',
        'AR': 'Arabic',
        'HI': 'Hindi',
      }
    };
  },
  mounted() {
    this.getStories()
  },
  methods: {
    getStories() {
      axios
        .get(`/api/v1/story`)
        .then(response => {
          this.stories = response.data
          console.log(this.stories[0])
        })
        .catch(error => {
          console.log(JSON.stringify(error))
        })
    }
  }
}
</script>

<style>
.card {
  text-decoration: none; /* Removes underline from all router links */
}

.row {
  padding-left: 30px;  /* Adjust the size as needed */
  padding-right: 30px; /* Adjust the size as needed */
}
</style>