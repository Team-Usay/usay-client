<template>
  <v-container>
    <!-- 좌측 네비게이션 바 부분 -->
    <v-navigation-drawer>
      <v-list-item title="Records"></v-list-item>
      <v-divider></v-divider>
      <v-list-item v-for="(roomName, index) in roomNames" :key="index">
        <v-list-item>{{ roomName.value }}</v-list-item>
      </v-list-item>
    </v-navigation-drawer>

    <v-card class="chat-box" flat>
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
            append-icon="mdi-robot-happy-outline"
            elevation="4"
          >
            <v-card-text align="right">{{ message.text }}</v-card-text>
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
      if (this.newMessage.trim() !== "") {
        this.messages.push({ isUser: true, text: this.newMessage });
        this.messages.push({ isUser: false, text: this.newMessage });
        this.newMessage = ""; // 메시지 전송 후 입력 필드를 비웁니다.
        this.roomNames.push({ value: "hello" });
      }
    },
  },
};
</script>

<style>
.flex {
  display: flex;
}

.align-center {
  align-items: center;
}
</style>
