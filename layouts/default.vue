<template>
  <v-app dark>
    <v-navigation-drawer
      :mini-variant="miniVariant"
      permanent
      app
      dark
    >
      <h3 class="text-center ma-5">
        <nuxt-link to="/" class="title drawer-title">НОВОСТИ</nuxt-link>
      </h3>

      <v-list class="pa-0">
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <v-container class="col">
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          icon: "mdi-home-outline",
          title: "Главная",
          to: "/"
        },
        {
          icon: "mdi-newspaper-variant-outline",
          title: "Новостная лента",
          to: "/news"
        }
      ],
    };
  },
  mounted() {
    this.$store.dispatch("news/getNews");
  },
  computed: {
    miniVariant() {
      switch (this.$vuetify.breakpoint.name) {
        case "xs":
          return true;
        case "sm":
          return true;
        case "md":
          return true;
        case "lg":
          return false;
        case "xl":
          return false;
      }
      return this.miniVariant;
    }
  }
};
</script>

<style scoped>
.drawer-title {
  text-decoration: none;
  color: #fff;
}
</style>
