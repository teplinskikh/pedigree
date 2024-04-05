<template>
  <div class="gallery">
    <div class="gallery__selected">
      <img 
        class="gallery__selected__image" 
        :src="images[selectedImage].url" 
        :alt="images[selectedImage].title" 
      />
      <div class="gallery__selected__text">
        <h3> {{ images[selectedImage].title }}</h3>
        <p>{{ images[selectedImage].description }}</p>
      </div>
    </div>
    <div class="carousel">
      <div 
        class="carousel__arrow" 
        v-show="images.length > 1"
        @click="() => prevImage()" 
      >
        &lt;
      </div>
      <div 
        class="carousel__image-container" 
        v-for="(image, index) in images" 
        :key="image.id" 
        @click="() => updateSelectedImage(index)"
      >
        <img 
          class="carousel__image-container__image" 
          :src="image.url" :alt="image.title" 
          :class = "{'carousel__image-container__image__active' : index === selectedImage}" 
        />
      </div>
      <div 
        class="carousel__arrow" 
        v-show="images.length > 1"
        @click="() => nextImage()" 
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
  data () {
    return {
      selectedImage: 0
    }
  },
  methods: {
    updateSelectedImage(index) {
      this.selectedImage = index
    },
    prevImage() {
      if (this.selectedImage > 0) {
        this.selectedImage = this.selectedImage - 1
      } else {
        this.selectedImage = this.images.length - 1
      }
    },
    nextImage() {
      if (this.selectedImage < this.images.length - 1) {
        this.selectedImage = this.selectedImage + 1
      } else {
        this.selectedImage = 0
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

  &__selected {
    text-align: center;
    position: relative;
  
    &__image {
      max-width: 100%;
      max-height: 70vh;
    }

    &__text {
      position: absolute;
      bottom: 0;
      width: 100%;
      background-color: rgba(256,256,256,0.65)
    }
  }

  &__carousel {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 20px;
  }
}
  
.carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;

  &__image-container {
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

  &__arrow {
    background-color: #ccc;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }
}
</style>
