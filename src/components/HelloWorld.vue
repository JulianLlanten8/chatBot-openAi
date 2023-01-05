<script setup>
import { Configuration, OpenAIApi } from "openai";
const configuration = new Configuration({
  apiKey: import.meta.env.VITE_OPENAI_API_KEY,
});
console.log(import.meta.env.VITE_OPENAI_API_KEY);
const openai = new OpenAIApi(configuration);
const response = await openai
  .createCompletion({
    model: "text-davinci-002",
    prompt: "como puedo alimentar o actual?",
  })
  .then((response) => {
    console.log(response);
    return response;
  })
  .catch((error) => {
    console.log(error);
  });
const mensaje = "la respuesta de la api de openai es:";
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>{{ mensaje }}</h3>
    <div v-html="response.data.choices[0].text"></div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
