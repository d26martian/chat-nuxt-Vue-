<template>
  <div class="c-wrap">
    <div class="c-wrap__chat" ref="block">
      <Message
        v-for="m in messages"
        :key="m.text"
        :text="m.text"
        :name="m.name"
        :owner="m.id === user.id"
      />
    </div>
    <div class="c-wrap__form">
      <ChatForm />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import Message from "../components/Message";
import ChatForm from "../components/ChatForm";

export default {
  middleware: ["chat"],
  head(){
      return {
          title: `Комната ${this.user.room}`
      }
  },
  components: {
      Message,
      ChatForm
  },
  computed: mapState(["user", "messages"]),
  watch: {
      messages() {
        setTimeout(() => {
            this.$refs.block.scrollTop = this.$refs.block.scrollHeight
        })
      }
  }
}
</script>
<style scoped lang="scss">
  .c-wrap {
    height: 100%;
    position: relative;
    overflow: hidden;

    &__form {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      padding: 1rem;
      height: 80px;
      background: #212121;
    }

    &__chat {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 80px;
      padding: 1rem;
      overflow-y: auto;
    }
  }
</style>
