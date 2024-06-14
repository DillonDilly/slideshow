<template>
  <div id="app">
    <div class="logo">
      <img src="./assets/logo.jpg" alt="Logo" />
    </div>
    <div class="slideshow">
      <div
        v-for="(media, index) in mediaItems"
        :key="index"
        :class="['slide', { active: index === activeIndex }]"
      >
        <img
          v-if="media.type === 'image'"
          :src="media.src"
          :alt="'Slide ' + (index + 1)"
        />
        <video v-if="media.type === 'video'" autoplay muted loop>
          <source :src="media.src" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </div>
    </div>
    <p class="text">Mersvo</p>
  </div>
</template>

<script>
import img1 from "./assets/sponge.jpg";
import img2 from "./assets/minionsimps.jpg";
import img3 from "./assets/David.jpg";
import vid1 from "./assets/downloadd.mp4"; // Import your video file

export default {
  name: "App",
  data() {
    return {
      mediaItems: [
        { type: "video", src: vid1 }, // Add the video to the array
        { type: "image", src: img1 },
        { type: "image", src: img2 },
        { type: "image", src: img3 },
      ],
      activeIndex: 0,
      intervalId: null,
    };
  },
  mounted() {
    this.startSlideshow();
  },
  methods: {
    startSlideshow() {
      this.changeSlide(); // Start the slideshow
    },
    changeSlide() {
      clearInterval(this.intervalId);

      const currentMedia = this.mediaItems[this.activeIndex];
      const duration = currentMedia.type === "video" ? 30000 : 10000; // 30 seconds for video, 10 seconds for images

      this.intervalId = setInterval(() => {
        this.activeIndex = (this.activeIndex + 1) % this.mediaItems.length;
        this.changeSlide(); // Set the next slide's interval
      }, duration);
    },
  },
  beforeUnmount() {
    clearInterval(this.intervalId); // Clear the interval on component destroy
  },
};
</script>

<style>
#app {
  position: relative;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.logo {
  position: absolute;
  top: 10px;
  left: 10px;
}

.logo img {
  width: 300px; /* Adjust the size of the logo as needed */
  height: auto;
}

.slideshow {
  width: 70%; /* Adjust the width as needed */
  height: 70%; /* Adjust the height as needed */
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.slide {
  width: 100%; /* Make the slide take full width of the slideshow container */
  height: 100%; /* Make the slide take full height of the slideshow container */
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: opacity 1s ease-in-out;
  position: absolute; /* Position absolute to overlap slides */
}

.slide img,
.slide video {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

.slide.active {
  opacity: 1;
}

.text {
  position: absolute;
  bottom: 10px;
  left: 10px;
  color: red;
  font-size: 70px;
  z-index: 10;
}
</style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.header {
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}

nav {
  display: flex;
  flex-direction: column;
}

nav a {
  color: white;
  padding: 10px;
  text-decoration: none;
}

/* Styles for screens wider than 600px */
@media screen and (min-width: 600px) {
  nav {
    flex-direction: row;
    justify-content: center;
  }

  nav a {
    margin: 0 10px;
  }
}

/* Styles for screens wider than 900px */
@media screen and (min-width: 900px) {
  .container {
    display: flex;
    justify-content: space-between;
  }

  .content, .sidebar {
    padding: 20px;
  }

  .content {
    flex: 3;
  }

  .sidebar {
    flex: 1;
    background-color: #f4f4f4;
  }
}