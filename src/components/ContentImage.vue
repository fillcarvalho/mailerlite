<template>
  <div>
    Image Pos: {{ $attrs.refPosition }}
    <div class="" v-if="isOpen">
        <Carousel id="gallery" v-bind="galleryConfig" v-model="currentSlide">
    <Slide v-for="image in images" :key="image.id">
      <img :src="image.url" alt="Gallery Image" class="gallery-image" />
    </Slide>
  </Carousel>

  <Carousel id="thumbnails" v-bind="thumbnailsConfig" v-model="currentSlide">
    <Slide v-for="image in images" :key="image.id">
      <template #default="{ currentIndex, isActive }">
        <div
          :class="['thumbnail', { 'is-active': isActive }]"
          @click="slideTo(currentIndex)"
        >
          <img :src="image.url" alt="Thumbnail Image" class="thumbnail-image" />
        </div>
      </template>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import "vue3-carousel/carousel.css";
import { Carousel, Slide, Navigation } from "vue3-carousel";

export default {
  name: "ContentImage",
  components: { Carousel, Slide, Navigation },
  setup() {
    const isOpen = ref(false);

    const currentSlide = ref(0);
    const slideTo = (nextSlide) => (currentSlide.value = nextSlide);

    const galleryConfig = {
      itemsToShow: 1,
      wrapAround: true,
      slideEffect: "fade",
      mouseDrag: false,
      touchDrag: false,
      height: 320,
    };

    const thumbnailsConfig = {
      height: 80,
      itemsToShow: 6,
      wrapAround: true,
      touchDrag: false,
      gap: 10,
    };

    const images = Array.from({ length: 3 }, (_, index) => ({
      id: index + 1,
      url: `https://picsum.photos/800/600?random=${index + 1}`,
    }));

    const toJson = () => {
      return {
        type: "ContentImage",
        currentSlide
      };
    };

    return {
      isOpen,
      toJson,
      images,
      currentSlide,
      slideTo,
      galleryConfig,
      thumbnailsConfig,
      images,
    };
  },
};
</script>

<style scoped></style>
