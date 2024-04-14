<template>
  <v-sheet
    class="d-flex align-center justify-center flex-wrap text-center mx-auto px-4"
    height="80%"
    width="100%"
  >
    <div>
      <h2 class="text-h4 font-weight-black text-orange">Hi there!</h2>
      <div class="text-h5 font-weight-medium mb-2">
        <b class="text-orange">USAY</b> helps you to improve job interview
        skills.
      </div>

      <p class="text-body-2 mb-4">
        Click the button below to start your interview.
      </p>
      <!-- 여기에 채팅 목록 보여주기 -->

      <v-btn
        :loading="loading"
        class="flex-grow-1"
        height="48"
        variant="text"
        @click="load"
        prepend-icon="mdi-account-arrow-right-outline"
      >
        <template v-slot:prepend>
          <v-icon color="orange"></v-icon>
        </template>

        <router-link to="/chat" class="text-black" style="text-decoration: none;"
          ><b>Start an Interview</b></router-link
        >
      </v-btn>
    </div>
  </v-sheet>
</template>

<script>
export default {
  name: "HomeView",
};
</script>
