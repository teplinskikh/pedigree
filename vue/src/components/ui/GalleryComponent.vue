<template>
  <div class="gallery">
    <div class="selected">
      <img 
        class="selected__image" 
        :src="selectedImage.url" 
        :alt="selectedImage.title" 
      />
      <h3>{{ selectedImage.title }}</h3>
      <p>{{ selectedImage.description }}</p>
    </div>
    <div class="carousel">
      <div 
        class="arrow" 
        @click="prevImage" 
        v-show="images.length > 1"
      >
        &lt;
      </div>
      <div 
        class="image-container" 
        v-for="image in images" 
        :key="image.id" 
        @click="updateSelectedImage(image)"
      >
        <img 
          class="image-container__image" 
          :src="image.url" :alt="image.title" 
          :class = "{'image-container__image__active' : image === selectedImage}" />
      </div>
      <div 
        class="arrow" 
        @click="nextImage" 
        v-show="images.length > 1"
      >
        &gt;
      </div>
    </div>
  </div>
</template>
    
<script>
export default {
  name: 'GalleryComponent',
  props: {
    images: Array
  },
  data() {
    return {
      selectedImage: null
    };
  },
  mounted() {
    this.selectedImage = this.images[0]
  },
  methods: {
    updateSelectedImage(image) {
      this.selectedImage = image
    },
    prevImage() {
      const index = this.images.indexOf(this.selectedImage)
      if (index > 0) {
        this.selectedImage = this.images[index - 1]
      } else {
        this.selectedImage = this.images[this.images.length - 1]
      }
    },
    nextImage() {
      const index = this.images.indexOf(this.selectedImage)
      if (index < this.images.length - 1) {
        this.selectedImage = this.images[index + 1]
      } else {
        this.selectedImage = this.images[0]
      }
    }
  }
}
</script>
    
<style scoped lang="less">
.gallery {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  box-sizing: border-box;
  padding: 20px;
}
  
.selected {
  text-align: center;
  
  &__image {
    max-width: 100%;
    max-height: 70vh;
  }
}
  
.carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}
  
.image-container {
  margin: 0 5px;
  cursor: pointer;
  
  &__image {
    max-width: 100%;
    max-height: 50vh;
  
    &__active {
      transform: scale(1.1);
    }
  }
}
 
.arrow {
  background-color: #ccc;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
</style>