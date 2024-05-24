<template>
  <div class="child-component">
    <input v-model="inputData" type="text" placeholder="Masukkan data">
    <button class="send-button" @click="sendDataToParent">Kirim Data dari B</button>
  </div>
</template>

<script>
export default {
  name: 'ChildComponentB',
  data() {
    return {
      inputData: ''
    };
  },
  methods: {
    sendDataToParent() {
      if (this.inputData.trim() !== '') {
        this.$emit('data-from-b', this.inputData);
        this.inputData = ''; // Reset input field
      }
    }
  }
};
</script>

<style scoped>
.child-component {
  margin: 30px;
  padding: 35px;
  background: linear-gradient(135deg, #1857c2, #b2bec3);
  border-radius: 20px;
  text-align: center;
  border: 2px solid #6c5ce7;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
  transition: transform 0.4s ease, box-shadow 0.4s ease;
}

.child-component:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
}

input {
  margin-bottom: 15px;
  padding: 10px;
  width: 80%;
  border: 1px solid #2f18dc;
  border-radius: 5px;
}

.send-button {
  padding: 15px 30px;
  background-color: #a29bfe;
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 1.2em;
  font-weight: bold;
  text-transform: uppercase;
  transition: background-color 0.4s ease, transform 0.4s ease;
}

.send-button:hover {
  background-color: #7f8c8d;
  transform: scale(1.1);
}
</style>
