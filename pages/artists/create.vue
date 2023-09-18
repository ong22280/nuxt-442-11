<template>
  <h1 class="text-3xl">Add Artist</h1>
  <form @submit.prevent="onSubmit()">
    <div>
      <lable for="name"> Artist Name </lable>
      <p v-if="errorMessages">{{ errorMessages }}</p>
      <input type="input" id="name" v-model="formaDate.name" />
    </div>
    <div>
      <button type="submit">Submit</button>
    </div>
  </form>
</template>

<script setup lang="ts">
// import { useFetch } from '@vueuse/core'
// import { defineComponent, ref, useFetch } from '@nuxtjs/composition-api'

const formaDate = ref({
  name: "",
});
const errorMessages = ref<string>("");

async function onSubmit() {
  const { name } = formaDate.value;
  const {data: response, error} = await useFetch<any>("http://localhost/api/artist", {
    method: "POST",
    // body: JSON.stringify({ name }),
    body: { name, image_path: "image url" }
  });

  console.log(response.value);

  if (response !== null) {
    await navigateTo(`/artists/${response.value.id}`);
  } else {
    const { message,data } = error.value!;
    // alert(message);
    errorMessages.value = data.message;
  }
}
</script>
