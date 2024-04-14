<template>
  <v-sheet
    class="d-flex align-center justify-center flex-wrap text-center mx-auto px-4"
    height="80%"
    max-height="60%"
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

      <v-btn
        :loading="loading"
        class="flex-grow-1"
        height="48"
        rounded
        @click="load"
        variant="tonal"
        prepend-icon="mdi-account-arrow-right-outline"
      >
        <template v-slot:prepend>
          <v-icon color="orange"></v-icon>
        </template>

        <router-link to="/chat" class="text-black" style="text-decoration: none"
          ><b>Start an Interview</b></router-link
        >
      </v-btn>
    </div>
  </v-sheet>

  <v-sheet
    class="d-flex align-center justify-center flex-wrap text-center mx-auto px-4"
    width="100%"
  >
    <div>
      <div class="text-h7 font-weight-medium mb-2">
        Previous interview records can be found below.
      </div>

      <v-list-item v-for="(record, index) in records" :key="index">
        <v-row>
          <!-- 첫 번째 열: 제목과 날짜 -->
          <v-col cols="8">
            <p>
              <b> {{ record.title }} </b>
            </p>
            <p>{{ record.date }}</p>
          </v-col>
          <!-- 두 번째 열: 버튼 -->
          <v-col cols="4">
            <v-btn
              variant="tonal"
              rounded
              append-icon="mdi-arrow-right"
            >
              <router-link
                to="/chat"
                class="text-black"
                style="text-decoration: none"
                >move</router-link
              >
            </v-btn>
          </v-col>
        </v-row>
      </v-list-item>
    </div>
  </v-sheet>
</template>

<script>
export default {
  name: "HomeView",

  data() {
    return {
      records: [
        {
          title: "LLM Interview",
          date: "2024-01-01",
        },
        {
          title: "Spring Boot Interview",
          date: "2024-01-02",
        },
      ],
    };
  },
};
</script>
