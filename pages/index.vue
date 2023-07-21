<template>
  <div>
    <v-row>
      <v-col
        style="padding-right: 0px"
        class="container d-flex justify-start align-start"
        md="2"
      >
        <v-sheet color="#E5E7EB" class="container float-left" width="260">
          <v-row class="container">
            <v-col>
              <v-img :src="logo" width="40" height="20" class="mb-2"> </v-img>
              <v-btn
                variant="text"
                color="#E5E7EB"
                block
                rounded = "xl"
                elevation="0"
                :class="{ 'clicked-class': isClicked }"
                @click="setIndoxData"
                class="text-case-normal"
              >
                <img left :src="inboxIcon" class="icon-class" />
                Inbox
                <p class="mt-4 ml-16 text-red">{{ inboxes.length }}</p>
              </v-btn>
              <v-btn
                variant="text"
                color="#E5E7EB"
                block
                elevation="0"
                rounded = "xl"
                :class="{ 'clicked-class': isArchiveClicked }"
                @click="setArchiveData"
                class="text-case-normal text-red"
              >
                <img left :src="archive" class="icon-class" />
                Archive
                <p class="mt-4 ml-13 text-red">{{ archives.length }}</p>
              </v-btn>
            </v-col>
            <div class="d-flex align-end">
              <v-btn
                variant="text"
                color="#E5E7EB"
                block
                rounded = "xl"
                elevation="0"
                class="text-case-normal text-red"
              >
                <img left :src="logOutIcon" class="icon-class" />
                Logout
              </v-btn>
            </div>
          </v-row>
        </v-sheet>
      </v-col>
      <v-col style="padding-right: 0px; padding-left: 0px">
        <v-sheet>
          <p class="text-h4 ma-4">{{ title }}</p>
          <v-row class="ml-1">
            <v-col>
              <label class="form-control">
                <input
                  type="checkbox"
                  name="checkbox"
                  v-model="checkbox1"
                  @click="selectAllEmails"
                />
                Email Selected({{ numberOFSelection }})
              </label>
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

          <div class="">
            <MyCheckBox
              :isChecked="element.selected"
              :email="element.email"
              :body="element.body"
              @handelEmit="handelFunction"
              v-for="(element, index) in emails"
              :key="index"
            />
          </div>
        </v-sheet>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
const logo = ref(require("@/assets/logo.svg"));
const inboxIcon = ref(require("@/assets/inbox-icon.svg"));
const archive = ref(require("@/assets/archive.svg"));
const logOutIcon = ref(require("@/assets/log-out-04-icon.svg"));
const readIcon = ref(require("@/assets/read-icon.svg"));
const archiveIcon = ref(require("@/assets/archine-icon.svg"));
const isClicked = ref(false);
const checkbox1 = ref(false);
const title = ref("Inbox");
const clicked = ref(0);
const counter = ref(2)
const numberOFSelection = ref(0);
const isArchiveClicked = ref(false);
const handelFunction = (isSelected) => {
  console.log("in third", clicked.value);
  if (isSelected == 1) {

    numberOFSelection.value += 1;
  } else {
    numberOFSelection.value -= 1;

    if (numberOFSelection.value < 0) {

      numberOFSelection.value += counter.value;
      counter.value++;
    }
  }

  console.log("the value of selsect all", checkbox1.value);
  console.log("there is an emits", isSelected, numberOFSelection.value);
};
const inboxes = ref([
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
]);
const archives = ref([
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
  {
    email: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.",
    selected: false,
    body: "Lorem ipsum dolor sit amet, consectetur adipisicing elit.Eius aperiam officia ad veritatis illum ipsum reiciendis natus. Enim numquam, libero fugit nam officia esse delectus. Amet, assumenda? Nemo, tempora sed.",
  },
]);
onMounted(() => {
  emails.value = inboxes.value;
  isClicked.value = true;
  console.log("in refresh");
});
const emails = ref([]);
const selectAllEmails = () => {
  if (checkbox1.value == true) {
    for (let i = 0; i < emails.value.length; i++) {
      emails.value[i].selected = false;

      numberOFSelection.value = 0;
      console.log(i, emails.value[i].selected);
    }
  } else {
    for (let i = 0; i < emails.value.length; i++) {
      if (numberOFSelection.value != emails.value.length) {
        numberOFSelection.value++;
      }
      emails.value[i].selected = true;

      console.log(i, emails.value[i].selected, numberOFSelection.value);
    }
  }
};
const setIndoxData = () => {
  isClicked.value = !isClicked.value;
  isArchiveClicked.value = false;
  emails.value = inboxes.value;
  title.value = "Inbox";
};
const setArchiveData = () => {
  isArchiveClicked.value = !isArchiveClicked.value;
  isClicked.value = false;
  emails.value = archives.value;
  title.value = "Archive";
};
</script>
<style scoped>
.container {
  height: 100vh;
}

.icon-class {
  height: 24px;
  width: 24px;
  margin-right: 10px;
}
.text-case-normal {
  text-transform: none !important;
  color: black;
}

.clicked-class {
  font-weight: bold;
  background-color: #d6e2fb !important;
}

.form-control {
  font-size: 1rem;
  font-weight: bold;
  line-height: 1.1;
  display: grid;
  grid-template-columns: 1em auto;
  gap: 0.5em;
}
</style>
