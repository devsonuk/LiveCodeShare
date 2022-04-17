<template>
  <v-app>
    <v-app-bar app color="dark" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Logo"
          class="shrink mr-2"
          style="filter: invert(1)"
          contain
          src="@/assets/logo-small.png"
          transition="scale-transition"
          width="40"
        />

        <!-- <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        /> -->
        <h4 class="display-1">Code Collaboration</h4>
      </div>

      <v-spacer></v-spacer>
      <Poptip title="Title" content="content" placement="bottom-end">
        <Avatar size="large" :style="{ background: 'green' }">
          {{ "SK" }}
        </Avatar>
      </Poptip>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>

<style scoped>
.theme--dark.v-app-bar.v-toolbar.v-sheet {
  background-color: #003847;
  box-shadow: 0px 1px 1px -1px rgb(0 0 0 / 20%),
    0px 1px 1px 0px rgb(0 0 0 / 14%), 0px 1px 2px 0px rgb(0 0 0 / 12%);
}
</style>
