<template>
  <div id="app">
    <div class="header"></div>
    <div class="container">
      <div v-if="errored">Sorry, something went wrong, try again.</div>

      <div v-else>
        <div>
          <input type="text" placeholder="Search for a Photo" />
        </div>
        <div v-if="loading">loading...</div>

        <div v-else>
          <div class="photos">
            <div v-for="(photo, idx) in info" :key="idx" class="photo">
              <img :src="photo.urls.small" alt="" />
              <div class="photo-data">
                <div class="photo-name">{{ photo.user.name }}</div>
                <div class="photo-author">{{ photo.user.location }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      info: null,
      loading: false,
      errored: false,
    };
  },

  mounted() {
    axios
      .get(
        "https://api.unsplash.com/photos/?client_id=Tbt93pi1s83atkRNJPIkLrIKkjCksONI8QYzGnW1JE0"
      )
      .then((response) => {
        this.info = response.data;
        console.log(response);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>

<style>
body {
  margin: 0;
}

.container {
  padding: 5rem 5rem;
}

.header {
  background: #dce2e9;
  height: 35%;
  width: 100vw;
  position: absolute;
  z-index: -1;
}

.photos {
  width: 100vw;
  display: grid;
  padding: 0 5rem;
  justify-content: center;
  grid-template-columns: 1fr 1fr 1fr;
}

.photo {
  border-radius: 20px;
}
</style>
