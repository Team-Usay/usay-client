<template>
  <v-container>
    <div style="height: 85vh">
      <!-- 뒤로가기 버튼 -->
      <v-btn variant="text" color="orange" @click="$router.go(-1)">
        <v-icon left>mdi-arrow-left</v-icon>
        Back
      </v-btn>

      <div ref="messageList" style="overflow-y: auto; max-height: 100%">
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
                <v-card-text class="typewriter">{{ message.text }}</v-card-text>
              </v-card>
            </v-list-item>
          </template>
        </v-list>
      </div>
    </div>
    <v-divider></v-divider>

    <div>
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

import axios from "axios";

export default {
  name: "Chat",

  data() {
    return {
      messages: [],
      writingMessage: "",
    };
  },

  created() { // 처음 입장 시 질문 조회
    console.log("created")
    axios
          .get(process.env.VUE_APP_API_SERVER + "/api/v1/chats/init")

          .then(function (response) {
            const answer = response.data.data.answer;
            this.messages.push({ isUser: false, text: answer });
          })
          .catch(function (error) {
            console.error(error);
          });
  },

  methods: {
    scrollMessageListToBottom() {
      // $refs를 사용하여 messageList 요소에 접근
      const messageList = this.$refs.messageList;

      this.$nextTick(() => {
        // 스크롤을 아래로 내리기
        messageList.scrollTop = messageList.scrollHeight;
      });
    },

    sendMessage() {
      if (this.writingMessage.trim() !== "") {
        this.messages.push({ isUser: true, text: this.writingMessage });
        axios
          .post(
            process.env.VUE_APP_API_SERVER + "/api/v1/chats/ask",
            {
              answer: this.writingMessage,
            },
            {
              "Content-Type": "application/json",
            }
          )
          .then(function (response) {
            const answer = response.data.data.answer;
            this.messages.push({ isUser: false, text: answer });
          })
          .catch(function (error) {
            console.error(error);
          });
          
        this.writingMessage = "";
      }
      this.scrollMessageListToBottom();
    },
  },
};
</script>