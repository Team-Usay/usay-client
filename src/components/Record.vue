<template>
  <div class="pa-4 text-center" scrollable>
    <v-dialog max-width="800">
      <template v-slot:activator="{ props: activatorProps }">
        <v-btn
          variant="tonal"
          rounded
          v-bind="activatorProps"
          text="watch"
        ></v-btn>
      </template>

      <template v-slot:default="{ isActive }">
        <v-card title="Spring Boot Interview" subtitle="2024-01-02">
          <v-list>
            <v-list-item v-for="(message, index) in messages" :key="index">
              <v-card
                v-if="message.isUser"
                prepend-icon="mdi-account"
                elevation="4"
              >
                <v-card-text max-width="100">{{ message.text }}</v-card-text>
              </v-card>

              <v-card
                v-if="!message.isUser"
                prepend-icon="mdi-robot-happy-outline"
                elevation="4"
              >
                <v-card-text class="typewriter">{{ message.text }}</v-card-text>
              </v-card>
            </v-list-item>
          </v-list>
          <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn
              color="surface-variant"
              text="Close"
              variant="flat"
              @click="isActive.value = false"
            ></v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Record",

  data() {
    return {
      messages: [
        {
          isUser: false,
          text: "백엔드 서버에서 사용하는 주요 프로그래밍 언어는 무엇이 있나요?",
        },

        {
          isUser: true,
          text: "Java나 Python이 있습니다.",
        },
        {
          isUser: false,
          text: "좋아요, Java와 Python이 백엔드 서버 개발에서 많이 사용되는 언어 중 하나라는 건 알고 있어요. 그렇다면 이 두 언어 중에서 어떤 기준으로 선택을 하게 되는지 알려주실 수 있나요?",
        },

        {
          isUser: true,
          text: "Python의 경우 인터프리터 언어이며, 배우기 쉽다는 장점이 있습니다. 따라서 과학이나 머신러닝 등에서 주로 활용됩니다. Java는 대규모 분산 어플리케이션을 만들기 위해 주로 활용되며, Spring Boot라는 프레임워크를 사용해 웹 어플리케이션을 개발할 수 있습니다.",
        },
        {
          isUser: false,
          text:
            "네, Python은 배우기 쉽고 빠르게 프로토타이핑할 수 있는 장점이 있고, 데이터 과학이나 머신러닝 분야에서 많이 활용되는 언어입니다. 반면에 Java는 대규모 시스템이나 엔터프라이즈 애플리케이션을 개발하기에 적합하며, Spring Boot와 같은 프레임워크를 통해 강력한 웹 어플리케이션을 개발할 수 있습니다." +
            "그렇다면 백엔드 개발에 Python과 Java 중에서 어떤 언어를 선호하시는지, 그 이유가 무엇인지 알려주실 수 있나요?",
        },

        {
          isUser: true,
          text: "저는 Java를 선호하는데, 웹 어플리케이션 개발을 주로 하기 때문입니다. Java와 Spring Boot의 경우 웹 어플리케이션을 만들기 위한 편리한 라이브러리를 제공하며, 개발자는 추상적인 기술을 다루며 안정적인 어플리케이션을 구현할 수 있습니다.",
        }
      ],
    };
  },
});
</script>
