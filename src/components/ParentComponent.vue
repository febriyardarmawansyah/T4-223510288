<template>
  <div class="parent-component">
    <h2>Komponen Utama</h2>
    <p>Data yang Diterima: {{ receivedData }}</p>
    <ChildComponentA @data-from-a="handleDataFromA" />
    <ChildComponentB @data-from-b="handleDataFromB" />
    <NestedComponentC />
    <div class="slot-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import ChildComponentA from './ChildComponentA.vue';
import ChildComponentB from './ChildComponentB.vue';
import NestedComponentC from './NestedComponentC.vue';

export default {
  name: 'ParentComponent',
  components: {
    ChildComponentA,
    ChildComponentB,
    NestedComponentC
  },
  data() {
    return {
      receivedData: ''
    };
  },
  methods: {
    handleDataFromA(data) {
      this.receivedData = data;
    },
    handleDataFromB(data) {
      this.receivedData = data;
    }
  }
};
</script>

<style scoped>
.parent-component {
  border: 2px solid #ddd;
  border-radius: 10px;
  background-color: #ffffff;
  padding: 20px;
  text-align: center;
  margin-top: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.parent-component h2 {
  color: #333;
  font-size: 1.5em;
}

.parent-component p {
  color: #555;
  font-size: 1.1em;
  margin: 10px 0;
}

.slot-content {
  padding: 15px;
  background-color: #e6f7ff;
  border: 1px solid #91d5ff;
  border-radius: 8px;
  margin-top: 20px;
}
</style>
