<template>
  <div class="email " style="padding: 0;">
    <v-divider ></v-divider>
    <v-row class="  mt-5 mb-5 ml-3"  >

      <input
        class="form-control ml-1"
        type="checkbox"
        name="checkbox"
        :checked="isChecked"

        value="true"
        @click="handelFunction"
      />

      <label class="email d-flex form-control ml-1" @click="open = true" >
        {{ email }}
      </label>
    </v-row>
    <v-divider ></v-divider>
    <my-slide-bar :title="email" :body="body" :open="open" @handelOpen="handelOpenFunction"></my-slide-bar>
    <div></div>
  </div>
</template>
<script setup>
import { ref, defineProps, onMounted, onUnmounted, defineEmits } from "vue";

const count = ref(0);
const open = ref(false);
const props = defineProps({
  isChecked: {
    type: Boolean,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  body: {
    type: String,
    required: true,
  },
});
const emits = defineEmits(["handelEmit"]);
const handleKeyup = (event) => {
  if (event.key === "Escape") {
    open.value = false;
  } else if (event.key === "a") {
    open.value = false;
  }
};


const handelFunction = () => {
  if(count.value == 0){
    count.value = 1
  }else if(count.value ==1){
    count.value = 0
  }
  emits("handelEmit",count.value);

};
const handelOpenFunction = ()=>{
  open.value= false;
}
onMounted(() => {
  window.addEventListener("keyup", handleKeyup);
});

onUnmounted(() => {
  window.removeEventListener("keyup", handleKeyup);
});
</script>

<style scoped>
.form-control {
  font-size: 1rem;
  font-weight: bold;
  line-height: 1.1;
  display: grid;
  grid-template-columns: 1em auto;
  gap: 0.5em;
}
.email:hover{
cursor: pointer;
background-color: #CAD6E4;
}
</style>
