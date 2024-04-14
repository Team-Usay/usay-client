<template>
  <Chat/>
</template>

<script>
import { defineComponent } from 'vue';

import Chat from '../components/Chat.vue'

export default defineComponent({
  name: 'ChatView',

  components: {
    Chat,
  },
});
</script>
