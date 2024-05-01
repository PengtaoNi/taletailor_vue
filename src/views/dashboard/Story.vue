<template>
  <div class="page-edit-character">

    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="column is-12 has-text-centered py-3" style="font-family: mali-bold; text-align: center; color: #2b2f97;">{{ story.title }}</h1>
      </div>
    </div>

    <div id="storyCarousel" class="carousel slide" data-ride="carousel" data-bs-wrap="false" style="padding-bottom: 30px;">
      <div class="carousel-inner">
        <div v-for="(illustration, index) in story.illustrations" :key="illustration.id" :class="['carousel-item', { active: index === 0 }]">
          <img :src="illustration.image" :alt="'Illustration ' + (index + 1)" class="d-block carousel-image">
          <div class="caption-below">
            <p class="caption-text"  @mouseover="showTranslation(index)" @mouseleave="hideTranslation">
              <template v-if="translate">
                {{ getSceneTranslation(index) }}
              </template>
              <template v-else>
                {{ getSceneText(index) }}
              </template>
            </p>
          </div>
        </div>
      </div>
      <a href="#" class="carousel-control-prev enhanced-control" data-bs-target="#storyCarousel" role="button" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      </a>
      <a href="#" class="carousel-control-next enhanced-control" data-bs-target="#storyCarousel" role="button" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
      </a>
    </div>
    <div class="column is-12"><h1> </h1></div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Story',
  data() {
    return {
      story: {},
      translate: false
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
      return scenes[index].split('|')[0];
    },
    getSceneTranslation(index) {
      const scenes = this.story.text.split('\n');
      return scenes[index].split('|')[1];
    },
    showTranslation(index) {
      if (this.getSceneTranslation(index) != '') {
        this.translate = true;
      }
    },
    hideTranslation() {
      this.translate = false;
    }
  }
}
</script>

<style>
.carousel-item {
  position: relative;
  width: 100%;
  height: 83vh; /* Full viewport height */
}

.carousel-image {
  max-width: 60vh; /* Adjust this value based on your design needs */
  margin: auto; /* Center the image */
}

.carousel-fit {
  position: absolute;
  top: 50%;
  left: 50%;
  width: auto;
  height: 100vh;
  max-width: none;
  transform: translate(-50%, -50%);
  object-fit: cover;
}

.carousel-control-prev-icon,
.carousel-control-next-icon {
  filter: drop-shadow(20px 20px 40px #000); /* Shadow for visibility */
  background-color: #000;
  border-radius: 50%; /* Circular background */
}

.caption-below {
  text-align: center;
  transform: translate(10%, 0%);
  max-width: 80vw;
  margin-top: 20px; /* Space between the image and the caption */
}

.caption-text {
  font-family: mali-bold;
  font-size: 2.5vh;
  color: #2b2f97; /* White text for better visibility */
  text-shadow: 
    -1px -1px 0 #fff,  
    1px -1px 0 #fff,
    -1px 1px 0 #fff,
    1px 1px 0 #fff; /* Black text outline */
}

.enhanced-control {
  filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.7)); /* Shadow for visibility */
}
</style>