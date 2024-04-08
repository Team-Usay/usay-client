<template>
  <v-container>
    <!-- 좌측 네비게이션 바 부분 -->
    <v-navigation-drawer class="bg-blue-grey-lighten-4 rounded-e-lg border-0">
      <!-- <v-list-item link class="bg-blue-grey-lighten-3">new Chat</v-list-item> -->
      <v-list-item v-for="(roomName, index) in roomNames" :key="index">
        <v-list-item
          link
          class="border-b-sm"
          style="color: white; text-shadow: 0.5px 0.5px 0.5px #263238"
          >{{ roomName.value }}</v-list-item
        >
      </v-list-item>
    </v-navigation-drawer>

    <v-card flat>
      <v-list>
        <v-list-item v-for="(message, index) in messages" :key="index">
          <!-- 사용자 아이콘 + 텍스트 부분 -->

          <v-card
            v-if="message.isUser"
            prepend-icon="mdi-account"
            elevation="4"
          >
            <v-card-text max-width="100">{{ message.text }}</v-card-text>
          </v-card>

          <!-- AI 아이콘 + 텍스트 부분 -->
          <v-card
            v-if="!message.isUser"
            prepend-icon="mdi-robot-happy-outline"
            elevation="4"
          >
            <v-card-text class="typewriter">{{ message.text }}</v-card-text>
          </v-card>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-card-actions>
        <!-- 텍스트 필드 부분 -->
        <v-text-field
          v-model="newMessage"
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
    </v-card>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "Chat",
  data() {
    return {
      messages: [],
      roomNames: [],
      newMessage: "",
      currentUser: "USER", // 사용자 이름을 정의합니다.
    };
  },
  methods: {
    sendMessage() {
      this.messages.push({ isUser: true, text: this.newMessage });
      var interMessages = this.messages;
      if (this.newMessage.trim() !== "") {
        console.log(process.env.VUE_APP_API_SERVER)
        axios
          .post(
            process.env.VUE_APP_API_SERVER,
            {
              prompt: this.newMessage,
            },
            {
              "Content-Type": "application/json",
            }
          )
          .then(function (response) {
            console.log(response.data.data)
            var data = response.data.data;
            var modelIndex = data.indexOf("model");
            data = data.slice(modelIndex + "model".length);

            interMessages.push({ isUser: false, text: data });
          })
          .catch(function (error) {
            // 예외처리
            console.log(error);
          });

        this.newMessage = ""; // 메시지 전송 후 입력 필드를 비웁니다.
        // this.roomNames.push({ value: "스프링 부트 면접" });
      }
    },
  },
};
</script>
