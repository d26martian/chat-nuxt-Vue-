<template>
    <v-text-field
      label="Введите сообщение"
      v-model="text"
      @keydown.enter="send"
      outlined
    ></v-text-field>
</template>
<script>
export default {
    data: () => ({
        text: ''
    }),
    methods: {
        send() {
            this.$socket.emit('createMessage', {
                text: this.text,
                id: this.$store.state.user.id
            }, data => {
              if(typeof data === 'string') {
                  console.error(data);
              } else {
                  this.text = ''
              }
            })
        }
    }
}
</script>
