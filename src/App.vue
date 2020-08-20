<template>
    <div class="container">
        <button v-on:click="sendMessage('hello')">Send Message</button>
    </div>
</template>

<script>
  export default {
    data: function() {
      return {
        connection: null
      }
    },
    created: function() {
      var mqtt = require('mqtt')
      console.log("Starting connection to WebSocket Server")
      // this.connection = new WebSocket("wss://broker.mqttdashboard.com")
      this.connection = mqtt.connect('mqtt://test.mosquitto.org')

      this.connection.onmessage = function(event) {
        console.log(event);
      }

      this.connection.onopen = function(event) {
        console.log(event)
        console.log("Successfully connected to the echo websocket server...")
      }

    },
    methods: {
      sendMessage: function(message) {
        console.log(this.connection);
        this.connection.send(message);
      }
    },
    
  }
</script>

<style>

</style>
