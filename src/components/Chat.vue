<template>
  <v-container>
    <v-card class="chat-box" flat>
      <v-list>
        <v-list-item v-for="(message, index) in messages" :key="index">
          <div class="flex align-center">
            <v-avatar image="user_avartar.jpeg"></v-avatar>
            <v-list-item-content>
              <!-- <v-list-item-title>{{ message.user }}</v-list-item-title> -->
            </v-list-item-content>
          </div>
          <v-list-item-content>
            <v-list-item-title>{{ message.text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-card-actions>
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
      newMessage: "",
      currentUser: "user", // 사용자 이름을 정의합니다.
    };
  },
  methods: {
    sendMessage() {
      if (this.newMessage.trim() !== "") {
        this.messages.push({ user: this.currentUser, text: this.newMessage });
        this.newMessage = ""; // 메시지 전송 후 입력 필드를 비웁니다.
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
