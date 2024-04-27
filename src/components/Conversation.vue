<template>
  <v-list style="overflow-y: auto; max-height: 100%">
    <template v-if="messages.length !== 0">
      <v-list-item v-for="(message, index) in messages" :key="index">
        <!-- 사용자 아이콘 + 텍스트 부분 -->
        <v-card v-if="message.isUser" prepend-icon="mdi-account" elevation="4">
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

    <!-- 아무 메세지도 없을 시, Welcome 출력 -->
    <template v-else>
      <v-list-item style="height: 100%">
        <v-card flat style="height: 100%">
          <v-card-text class="fill-height d-flex align-center justify-center">
            <h2 class="text-h10 font-weight-black text-orange">
              Start a conversation
            </h2></v-card-text
          >
        </v-card>
      </v-list-item>
    </template>
  </v-list>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Conversation",
  props: ["messages"],
});
</script>