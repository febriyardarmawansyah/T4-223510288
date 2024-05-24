<template>
  <div class="nested-component" @click="toggleContent">
    <p>Komponen Nested C</p>
    <div class="slot-content" :class="{ 'show': showContent }" @click.stop>
      <slot></slot>
      <button class="toggle-button" @click.stop="toggleContent">{{ showContent ? 'Sembunyikan Konten' : 'Tampilkan Konten' }}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NestedComponentC',
  data() {
    return {
      showContent: false
    };
  },
  methods: {
    toggleContent() {
      this.showContent = !this.showContent;
    },
    showAlert() {
      alert('Ini adalah pesan dari Komponen Nested C!');
    }
  }
};
</script>

<style scoped>
.nested-component {
  padding: 20px;
  background-color: #f0f8ff;
  border-radius: 12px;
  text-align: center;
  margin-top: 20px;
  border: 2px solid #3498db;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.nested-component:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.nested-component p {
  color: #2980b9;
  font-size: 1.5em;
  margin: 0;
}

.slot-content {
  padding: 10px;
  background-color: #ffcccc;
  border-radius: 8px;
  margin-top: 15px;
  transition: background-color 0.3s ease;
  display: none;
}

.slot-content.show {
  display: block;
}

.toggle-button {
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #fdcb6e;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1em;
  transition: background-color 0.3s ease;
}

.toggle-button:hover {
  background-color: #ffaf40;
}
</style>
