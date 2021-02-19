<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app :mobile-breakpoint="768">
      <v-img
        class="pa-4 pt-4"
        src="mountains.jpg"
        height="150"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar size="70" class="mb-2">
          <img
            src="https://media-exp1.licdn.com/dms/image/C4E03AQEnw095aewvXA/profile-displayphoto-shrink_800_800/0/1516860964079?e=1617840000&v=beta&t=H7fwg5KVr2Og5zeL1b1YFvSfi5sxbfG6MjnZ9pv9iYU"
            alt="Sergio"
          />
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Sergio Servín Arce
        </div>
        <div class="white--text text-subtitle-2">serserar</div>
      </v-img>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      color="primary"
      src="mountains.jpg"
      app
      dark
      prominent
      :height="$route.path === '/' ?  '180' : '150' "
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class=" header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>

        <v-row>
          <v-app-bar-title class="text-h4 ml-4"> {{ $store.state.appTitle }} </v-app-bar-title>
        </v-row>

        <v-row>
          <live-date-time />
        </v-row>
        <v-row v-if="$route.path === '/'">
            <field-add-task />
        </v-row>

      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),

  mounted(){

    this.$store.dispatch('getTasks')
  },
  components: {
    snackbar: require("@/components/Shared/Snackbar.vue").default,
    search: require("@/components/Tools/Search.vue").default,
    "live-date-time": require("@/components/Tools/LiveDateTime.vue").default,
    'field-add-task' : require('@/components/Todo/FieldAddTask.vue').default
  },
};
</script>
<style lang="sass">
  .header-container
    max-width: none !important
</style>