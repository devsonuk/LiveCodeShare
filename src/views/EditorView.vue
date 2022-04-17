<template>
  <div class="code-playground">
    <v-navigation-drawer
      absolute
      dark
      mini-variant
      mini-variant-width="60"
      permanent
    >
      <v-list nav dense>
        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-folder</v-icon>
          </v-list-item-icon>
        </v-list-item>
        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-account-multiple</v-icon>
          </v-list-item-icon>
        </v-list-item>
        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-star</v-icon>
          </v-list-item-icon>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <div
      class="code-conatainer"
      :style="{ height: `${mainContainerHeight}px` }"
    >
      <CodeEditor :height="mainContainerHeight" :socket="socket" />
    </div>
    <v-btn
      class="mx-2"
      fab
      dark
      color="cyan"
      style="position: absolute; bottom: 20px; right: 20px"
    >
      <v-icon dark> mdi-chat </v-icon>
    </v-btn>
    <ChatBox :socket="socket" />
    <v-footer dark app color="rgb(0, 32, 42)">
      <div>This is the footer</div>
    </v-footer>
  </div>
</template>

<script>
import CodeEditor from "../components/CodeEditor.vue";
import ChatBox from "../components/ChatBox.vue";
import { io } from "socket.io-client";
// const socket = io("http://localhost:3000/");

export default {
  components: {
    CodeEditor,
    ChatBox,
  },
  data() {
    return {
      mainContainerHeight: 0,
      socket: io("http://localhost:3000/"),
    };
  },
  methods: {
    setHeight() {
      var navContainer = document.querySelector(".v-navigation-drawer");
      this.mainContainerHeight =
        navContainer != undefined ? navContainer.clientHeight - 33 : 500;
      console.log("mainContainerHeight", this.mainContainerHeight);
    },
  },
  destroyed() {
    window.removeEventListener("resize", this.setHeight);
  },
  mounted() {
    window.addEventListener("resize", this.setHeight);
    this.setHeight();
  },
};
</script>

<style scoped>
.code-conatainer {
  padding-left: 60px;
  padding-top: 0;
  padding-right: 0;
  padding-bottom: 0;
}
.theme--dark.v-navigation-drawer {
  background-color: #003847;
}
</style>
