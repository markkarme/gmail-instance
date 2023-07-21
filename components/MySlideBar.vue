<template>
  <div>
    <transition name="fade">
      <div v-if="isOpen" class="overlay" @click="closeSlide"></div>
    </transition>

    <transition name="slide">
      <div v-if="isOpen" class="sidenav">
        <!-- Add more navigation links here -->
        <v-row class="ml-1">
          <v-col class="d-flex">
            <img
              :src="closeIcon"
              width="19"
              height="19"
              class="mt-1 mr-1"
              @click="closeSlide"
            />
            <p style="color: #4b5563" class="mr-6">Close (Esc)</p>
          </v-col>
          <v-col class="d-flex justify-end mr-16">
            <img
              :src="readIcon"
              width="15.83"
              height="15.13"
              class="mt-1 mr-1"
            />
            <p style="color: #4b5563" class="mr-6">Mark as read(r)</p>
            <img
              :src="archiveIcon"
              width="15.83"
              height="15.13"
              class="mt-1 mr-1"
            />
            <p style="color: #4b5563">Archive(a)</p>
          </v-col>
        </v-row>
        <p class="text-h6 ml-4" style="color: #121829">{{ title }}</p>
        <p class="ml-4" style="color: #4b5563">{{ body }}</p>
      </div>
    </transition>

    <!-- Content goes here -->
  </div>
</template>

<script setup>
import { ref, defineProps, watchEffect ,defineEmits} from "vue";

const readIcon = ref(require("@/assets/read-icon.svg"));
const archiveIcon = ref(require("@/assets/archine-icon.svg"));
const closeIcon = ref(require("@/assets/x-close.svg"));
const emits = defineEmits(['handelOpen']);
const props = defineProps({
  open: {
    type: Boolean,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  body: {
    type: String,
    required: true,
  },

});
const isOpen = ref(props.open);

watchEffect(() => {
  isOpen.value = props.open;
});



const closeSlide =()=>{
  props.open = false;
  emits('handelOpen')
}
</script>

<style scoped>
.sidenav {
  height: 100%;
  width: 800px;
  position: fixed;
  z-index: 1;
  top: 0;
  right: 0;
  background-color: white;
  overflow-x: hidden;
  padding-top: 30px;
  transition: 0.5s;
}

.overlay {
  height: 100%;
  width: 100%;
  position: fixed;
  z-index: 1;
  top: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  transition: 0.5s;
}

/* Slide transition for the sidenav */
.slide-enter-active,
.slide-leave-active {
  transition: width 0.5s;
}

.slide-enter,
.slide-leave-to {
  width: 0;
}

.slide-enter-to,
.slide-leave {
  width: 800px;
}

/* Fade transition for the overlay */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-to,
.fade-leave {
  opacity: 1;
}
</style>
