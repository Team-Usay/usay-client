<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card flat>
          <v-list>
            <template v-if="messages.length !== 0">
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
                  <v-card-text class="typewriter">{{
                    message.text
                  }}</v-card-text>
                </v-card>
              </v-list-item>
            </template>

            <!-- 아무 메세지도 없을 시, Welcome 출력 -->
            <template v-else>
              <v-list-item style="height: 100%">
                <v-card flat style="height: 100%">
                  <v-card-text
                    class="fill-height d-flex align-center justify-center"
                    >Start a conversation...</v-card-text
                  >
                </v-card>
              </v-list-item>
            </template>
          </v-list>
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
        </v-card>
      </v-col>
    </v-row>
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
      writingMessage: "",
      isNavigationVisible: true,
    };
  },

  methods: {
    sendMessage() {
      // 컨텍스트 공유를 위한 변수
      const interMessages = this.messages;
      if (this.writingMessage.trim() !== "") {
        // 우선 유저가 보낸 메세지 저장
        this.messages.push({ isUser: true, text: this.writingMessage });
        // 프롬프트 요청
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
};
</script>
