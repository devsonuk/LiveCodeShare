<template>
  <div class="chat-box" v-show="showChatBox">
    <v-card class="mx-auto fill-height" width="100%">
      <v-card-title class="pt-2 pb-2">Messaging</v-card-title>
      <v-card-text class="chat-area">
        <v-container fluid style="padding: 0">
          <v-list disabled two-line style="background: transparent">
            <v-list-item-group>
              <v-list-item v-for="(item, i) in messages" :key="i">
                <!-- <v-list-item-icon>
                  <v-icon v-text="item.icon"></v-icon>
                </v-list-item-icon> -->
                <v-list-item-avatar>
                  <v-img
                    :src="'https://cdn.vuetifyjs.com/images/lists/2.jpg'"
                  ></v-img>
                </v-list-item-avatar>
                <v-list-item-content
                  style="
                    background: #f5f5f5;
                    border-radius: 12px;
                    padding: 10px;
                  "
                >
                  <v-list-item-title>{{ item.username }}</v-list-item-title>
                  <v-list-item-subtitle>{{ item.text }}</v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-container>
      </v-card-text>
      <v-footer style="padding: 1px">
        <Input
          v-model="message"
          placeholder="Write a message..."
          clearable
          type="textarea"
          :autosize="{ minRows: 2, maxRows: 6 }"
          style="width: 100%"
          @on-enter="sendMessage"
        />
      </v-footer>
    </v-card>
  </div>
</template>

<script>
export default {
  props: ["socket"],
  data() {
    return {
      showChatBox: true,
      messages: [],
      message: "",
    };
  },
  mounted() {
    var username = "Sonu";
    var roomId = this.$route.params.roomId;
    this.socket.emit("joinRoom", { username, roomId });

    this.socket.on("message", (payload) => {
      if (payload.text) {
        this.messages.push(payload);
      }
      console.log("Message Client", payload);
    });

    this.socket.on("roomUsers", (payload) => {
      console.log(payload);
    });
  },
  updated() {
    var chatArea = document.querySelector(".chat-area");
    chatArea.scrollTop = chatArea.scrollHeight;
  },
  methods: {
    sendMessage() {
      //Emitting a event to server
      if (this.message != "" && this.message != "\n") {
        this.socket.emit("chatMessage", { message: this.message });
        this.message = "";
      }
    },
  },
};
</script>

<style scoped>
.chat-box {
  position: absolute;
  width: 400px;
  bottom: 10px;
  right: 10px;
  min-height: 500px;
}
.chat-area {
  background-color: #e6eaea;
  padding: 0;
  height: 400px;
  overflow-y: scroll;
  scroll-behavior: smooth;
}
.message-box .v-text-field__details {
  display: none;
}
</style>
