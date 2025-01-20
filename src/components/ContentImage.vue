<template>
  <div draggable="true">
    <Carousel v-bind="galleryConfig" v-model="currentSlide">
      <Slide v-for="image in images" :key="image.id">
        <img :src="image.url" alt="Gallery Image" class="gallery-image" />
      </Slide>
    </Carousel>

    <Carousel v-bind="thumbnailsConfig" v-model="currentSlide" class="mt-2">
      <Slide v-for="image in images" :key="image.id">
        <template #default="{ currentIndex, isActive }">
          <div
            :class="['thumbnail', { 'is-active': isActive }]"
            @click="slideTo(currentIndex)"
          >
            <img
              :src="image.url"
              alt="Thumbnail Image"
              class="thumbnail-image"
            />
          </div>
        </template>
      </Slide>

      <template #addons>
        <Navigation>
        <template #prev>
          <span class="carousel__buttom">←</span>
        </template>
        <template #next>
          <span class="carousel__buttom">→</span>
        </template>
      </Navigation>
      </template>
    </Carousel>
  </div>
</template>

<script>
import { ref, watch, onBeforeMount } from "vue";
import "vue3-carousel/carousel.css";
import { Carousel, Slide, Navigation } from "vue3-carousel";

export default {
  name: "ContentImage",
  emits: ["content-update"],
  props: ["id", "currentImageId"],
  components: { Carousel, Slide, Navigation },
  setup(props, { emit }) {
    const currentSlide = ref(0);
    const currentImageAddress = ref("");

    const slideTo = (nextSlide) => {
      currentSlide.value = nextSlide;
    };

    const galleryConfig = {
      itemsToShow: 1,
      wrapAround: true,
      slideEffect: "fade",
      mouseDrag: false,
      touchDrag: false,
      height: 200,
    };

    const thumbnailsConfig = {
      height: 80,
      itemsToShow: 3,
      wrapAround: true,
      touchDrag: false,
      gap: 10,
    };

    const images = Array.from({ length: 3 }, (_, index) => ({
      id: index,
      url: `/src/assets/images/image_${index}.jpg`,
    }));

    onBeforeMount(() => {
      // Update the currentImage with the prop value
      currentSlide.value = props.currentImageId;
      // Emiting an event
      updateImageAddressByIndex(props.currentImageId);
    });

    watch(currentSlide, (currentSlideValue) => {
      updateImageAddressByIndex(currentSlideValue);
    });

    /**
     * Update the image id and url at the parent component
     * @param index
     */
    const updateImageAddressByIndex = (index) => {
      currentImageAddress.value = images[index] ?? null;
      if (currentImageAddress.value) {
        console.log("getImageAddressByIndex", images[index]);
        updateParent(currentImageAddress.value);
      }
    };

    /**
     * Updates the values at the parent
     *
     * @param newData
     */
    const updateParent = function (newData) {
      emit("content-update", {
        url: newData.url,
        imageId: newData.id,
        id: props.id,
      });
    };

    return {
      images,
      currentSlide,
      slideTo,
      galleryConfig,
      thumbnailsConfig,
      currentImageAddress,
    };
  },
};
</script>

<style scoped>
.carousel__buttom {
  @apply text-white
}
</style>
