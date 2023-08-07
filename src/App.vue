<template>
  <div class="chat-container">
    <div class="messages" ref="messagesContainer">
      <div
        v-for="message in messages"
        :key="message.id"
        class="message"
        :class="{
          me: message.sender === 'me',
          stranger: message.sender === 'stranger',
        }"
      >
        <div class="message-info">
          <div class="sender">{{ message.sender }}</div>
          <div class="date">{{ message.date }}</div>
          <div class="time">{{ message.time }}</div>
        </div>
        <div class="message-text">{{ message.text }}</div>
        <div class="button-container">
          <!-- <button class="like-button" @click="likeMessage(message.id)">
            
          </button> -->
          <button class="delete-button" @click="deleteMessage(message.id)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 100 100"
              width="26px"
              height="26px"
            >
              <path
                d="M 46 13 C 44.35503 13 43 14.35503 43 16 L 43 18 L 32.265625 18 C 30.510922 18 28.879517 18.922811 27.976562 20.427734 L 26.433594 23 L 23 23 C 20.802666 23 19 24.802666 19 27 C 19 29.197334 20.802666 31 23 31 L 24.074219 31 L 27.648438 77.458984 C 27.88773 80.575775 30.504529 83 33.630859 83 L 66.369141 83 C 69.495471 83 72.11227 80.575775 72.351562 77.458984 L 75.925781 31 L 77 31 C 79.197334 31 81 29.197334 81 27 C 81 24.802666 79.197334 23 77 23 L 73.566406 23 L 72.023438 20.427734 C 71.120481 18.922811 69.489078 18 67.734375 18 L 57 18 L 57 16 C 57 14.35503 55.64497 13 54 13 L 46 13 z M 46 15 L 54 15 C 54.56503 15 55 15.43497 55 16 L 55 18 L 45 18 L 45 16 C 45 15.43497 45.43497 15 46 15 z M 32.265625 20 L 43.832031 20 A 1.0001 1.0001 0 0 0 44.158203 20 L 55.832031 20 A 1.0001 1.0001 0 0 0 56.158203 20 L 67.734375 20 C 68.789672 20 69.763595 20.551955 70.306641 21.457031 L 71.833984 24 L 68.5 24 A 0.50005 0.50005 0 1 0 68.5 25 L 73.5 25 L 77 25 C 78.116666 25 79 25.883334 79 27 C 79 28.116666 78.116666 29 77 29 L 23 29 C 21.883334 29 21 28.116666 21 27 C 21 25.883334 21.883334 25 23 25 L 27 25 L 61.5 25 A 0.50005 0.50005 0 1 0 61.5 24 L 28.166016 24 L 29.693359 21.457031 C 30.236405 20.551955 31.210328 20 32.265625 20 z M 64.5 24 A 0.50005 0.50005 0 1 0 64.5 25 L 66.5 25 A 0.50005 0.50005 0 1 0 66.5 24 L 64.5 24 z M 26.078125 31 L 73.921875 31 L 70.357422 77.306641 C 70.196715 79.39985 68.46881 81 66.369141 81 L 33.630859 81 C 31.53119 81 29.803285 79.39985 29.642578 77.306641 L 26.078125 31 z M 38 35 C 36.348906 35 35 36.348906 35 38 L 35 73 C 35 74.651094 36.348906 76 38 76 C 39.651094 76 41 74.651094 41 73 L 41 38 C 41 36.348906 39.651094 35 38 35 z M 50 35 C 48.348906 35 47 36.348906 47 38 L 47 73 C 47 74.651094 48.348906 76 50 76 C 51.651094 76 53 74.651094 53 73 L 53 69.5 A 0.50005 0.50005 0 1 0 52 69.5 L 52 73 C 52 74.110906 51.110906 75 50 75 C 48.889094 75 48 74.110906 48 73 L 48 38 C 48 36.889094 48.889094 36 50 36 C 51.110906 36 52 36.889094 52 38 L 52 63.5 A 0.50005 0.50005 0 1 0 53 63.5 L 53 38 C 53 36.348906 51.651094 35 50 35 z M 62 35 C 60.348906 35 59 36.348906 59 38 L 59 39.5 A 0.50005 0.50005 0 1 0 60 39.5 L 60 38 C 60 36.889094 60.889094 36 62 36 C 63.110906 36 64 36.889094 64 38 L 64 73 C 64 74.110906 63.110906 75 62 75 C 60.889094 75 60 74.110906 60 73 L 60 47.5 A 0.50005 0.50005 0 1 0 59 47.5 L 59 73 C 59 74.651094 60.348906 76 62 76 C 63.651094 76 65 74.651094 65 73 L 65 38 C 65 36.348906 63.651094 35 62 35 z M 38 36 C 39.110906 36 40 36.889094 40 38 L 40 73 C 40 74.110906 39.110906 75 38 75 C 36.889094 75 36 74.110906 36 73 L 36 38 C 36 36.889094 36.889094 36 38 36 z M 59.492188 41.992188 A 0.50005 0.50005 0 0 0 59 42.5 L 59 44.5 A 0.50005 0.50005 0 1 0 60 44.5 L 60 42.5 A 0.50005 0.50005 0 0 0 59.492188 41.992188 z"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
    <div class="input-container">
      <input
        @keyup.enter="sendMessage"
        v-model="newMessage"
        placeholder="Text here..."
      />
      <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messages: [
        {
          id: Date.now(),
          sender: "stranger",
          text: "Hey! How are you doing?",
          date: new Date().toDateString(),
          time: new Date().toLocaleTimeString(),
        },
      ],
    };
  },
  methods: {
    sendMessage() {
      if (this.newMessage.trim() !== "") {
        const message = {
          id: Date.now(),
          sender: "me",
          text: this.newMessage,
          date: new Date().toDateString(),
          time: new Date().toLocaleTimeString(),
        };

        this.messages.push(message);
        this.newMessage = "";

        // scrolling to the latest message
        this.$nextTick(() => {
          this.$refs.messagesContainer.scrollTop =
            this.$refs.messagesContainer.scrollHeight;
        });

        // simulating receiving message from another sender after a delay
        setTimeout(() => {
          const response = {
            id: Date.now(),
            sender: "stranger",
            text: "Some response message...",
            date: new Date().toDateString(),
            time: new Date().toLocaleTimeString(),
          };
          this.messages.push(response);

          // scroll to the latest message
          this.$nextTick(() => {
            this.$refs.messagesContainer.scrollTop =
              this.$refs.messagesContainer.scrollHeight;
          });
        }, Math.floor(Math.random() * 6000) + 5000); // simulating random delay between 5-10 seconds
      }
    },
    deleteMessage(id) {
      this.messages = this.messages.filter((message) => message.id !== id);
    },
    likeMessage(id) {
      const message = this.messages.find((message) => message.id === id);
      //
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  font-family: Open Sans;
  font-weight: 500;
}

.chat-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  padding: 2rem;
}
.messages {
  justify-content: center;
  flex-grow: 1;
  overflow-y: scroll;
}

.message {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  margin-bottom: 2rem;
  background-color: #f2f2f2;
  border-radius: 2rem;
  flex-wrap: wrap;
  height: auto;
  max-width: fit-content;
  animation: addAnimation 2s ease-in-out;
  .message-text {
    margin-left: 1rem;
    padding: 0.5rem;
  }
  .message-info {
    font-weight: 300;
    padding-right: 0.7rem;
  }
}

@keyframes addAnimation {
  0% {
    opacity: 0;
    transform: translateY(50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
}

.message.me {
  margin-left: auto;
}

.me {
  background-color: rgb(219, 227, 230);
  .message-info {
    .sender {
      color: rgb(102, 160, 180);
    }
  }
}
.stranger {
  background-color: rgb(181, 232, 180);
  .message-info {
    .sender {
      color: rgb(60, 147, 69);
    }
  }
}

.message-info {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: baseline;
  color: #999;
  font-size: 0.8rem;

  .sender {
    margin: 1rem;
    font-weight: 600;
    font-size: 0.9rem;
  }
  .date {
    margin: 0.1rem;
  }
}

.button-container {
  display: flex;
  flex-direction: row;
}
.like-button,
.delete-button {
  margin-left: 1vw;
  padding: 0.6rem 1rem;
  border-radius: 0.6rem;
  cursor: pointer;
  border: none;
  background: rgb(247, 244, 240);
}

button:hover {
  background-color: lightgray;
}

.input-container {
  display: flex;
  align-items: center;
  justify-content: center;
}
.input-container input {
  flex-grow: 0.8;
  padding: 0.4rem 0.8rem;
  border-radius: 0.4rem;
  border: 1px solid #ccc;
  margin-right: 0.4rem;
  padding: 1rem;
  font-size: 1rem;
}

.input-container button {
  background-color: #4caf50;
  border: none;
  color: #fff;
  padding: 0.5rem 0.8rem;
  border-radius: 0.4rem;
  cursor: pointer;
  padding: 1rem;
  font-size: 1rem;
}
</style>
