<template>
  <v-app app>
    <v-navigation-drawer app v-model="drawer" mobile-break-point="650">
      <v-list subheader>
        <v-subheader>Список людей в комнате</v-subheader>

        <v-list-item
          v-for="u in users"
          :key="u.name"
          @click.prevent
        >
          <v-list-item-avatar>
            <v-img :src="u.avatar"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-text="u.name"></v-list-item-title>
          </v-list-item-content>

          <v-list-item-icon>
            <v-icon :color="u.id === user.id ? 'success accent-4' : 'grey'">mdi-wechat</v-icon>
          </v-list-item-icon>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-btn icon @click="exit">
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
      <v-toolbar-title>Чат комнаты {{user.room}}</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <div style="height: 100%">
        <nuxt />
      </div>
    </v-content>
  </v-app>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
export default {
    data: () => ({
        drawer: true,
        // users: [
        //     { id: 1, name: 'User 1', avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg', active: true },
        //     { id: 2, name: 'User 2', avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg', active: false },
        //     { id: 3, name: 'User 3', avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg', active: false }
        // ]
    }),
    computed: mapState(['user', 'users']),
    methods: {
        ...mapMutations(['clearData']),
        exit() {
            this.$socket.emit('userLeft', this.user.id, () => {
                this.$router.push('/?message=leftChat ');
                this.clearData();
            });
        }
    }
}
</script>
