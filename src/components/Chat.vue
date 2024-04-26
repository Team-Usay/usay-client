<template>
  <v-container>
    <v-row>
      <v-col>
        <Conversation :messages="this.messages"></Conversation>
        <v-divider></v-divider>
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
              <v-btn color="secondary" @click="sendMessage"> Send </v-btn>
            </template>
          </v-text-field>
        </v-card-actions>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

import Conversation from "./Conversation.vue"

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
      const interMessages = this.messages;
      if (this.writingMessage.trim() !== "") {
        this.messages.push({ isUser: true, text: this.writingMessage });

        axios
          .post(
            process.env.VUE_APP_API_SERVER,
            {
              prompt: this.writingMessage,
            },
            {
              "Content-Type": "application/json",
            }
          )
          .then(function (response) {
            const data = response.data.data;
            const modelIndex = data.indexOf("model");
            const modelAnswer = data.slice(modelIndex + "model".length);

            interMessages.push({ isUser: false, text: modelAnswer });
          })
          .catch(function (error) {
            console.error(error);
          });
        this.writingMessage = "";
      }
    },
  },

  components: {
    Conversation,
  }
};
</script>
