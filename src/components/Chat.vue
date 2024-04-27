<template>
  <v-container>
    <div style="height: 90vh;"> <!-- Conversation 부분의 부모 요소 -->
      <Conversation :messages="messages" style="height: 100%;"></Conversation>
    </div>
    <v-divider></v-divider>

    <div style="height: 10vh;"> <!-- Conversation 부분의 부모 요소 -->
    <v-card-actions>
      <!-- 텍스트 필드 부분 -->
      <v-text-field
        v-model="writingMessage"
        label="write an answer."
        flat
        rounded
        variant="solo-filled"
        @keyup.enter="sendMessage"
      >
        <template #append>
          <v-btn color="orange" @click="sendMessage"> Send </v-btn>
        </template>
      </v-text-field>
    </v-card-actions>
    </div>
  </v-container>
</template>

<script>
// import axios from "axios";

import Conversation from "./Conversation.vue";

export default {
  name: "Chat",

  data() {
    return {
      messages: [],
      writingMessage: "",
    };
  },

  methods: {
    sendMessage() {
      if (this.writingMessage.trim() !== "") {
        this.messages.push({ isUser: true, text: this.writingMessage });

        // axios
        //   .post(
        //     process.env.VUE_APP_API_SERVER,
        //     {
        //       prompt: this.writingMessage,
        //     },
        //     {
        //       "Content-Type": "application/json",
        //     }
        //   )
        //   .then(function (response) {
        //     const data = response.data.data;
        //     const modelIndex = data.indexOf("model");
        //     const modelAnswer = data.slice(modelIndex + "model".length);

        //     this.messages.push({ isUser: false, text: modelAnswer });
        //   })
        //   .catch(function (error) {
        //     console.error(error);
        //   });
        this.writingMessage = "";
      }
    },
  },

  components: {
    Conversation,
  },
};
</script>

<style scoped>
.card-actions {
  position: absolute;
  bottom: 0;
  right: 0;
}
</style>