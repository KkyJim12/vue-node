<template>
  <div id="app">
    <input type="text" v-model="text" />
    <button type="button" @click="sendText()">Send !!</button>
    <ul>
      <li v-for="show in message" :key="show.index">{{ show }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
      message: []
    };
  },
  sockets: {
    connect: function() {
      console.log("socket connected");
    },
    message: function(msg) {
      this.message.push(msg);
    }
  },
  methods: {
    sendText() {
      this.$socket.emit("message", this.text);
    }
  }
};
</script>
