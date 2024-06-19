<template>
  <div>
    <h1>Lista de Afazeres</h1>
    <input type="text" @change="addToList" v-model="text" />
    <ul>
      <li v-for="(item, index) in list" :key="index">
        <div @click="toggleCheckBox(item)">
          <input type="checkbox" :checked="item.checked" />
          <span :class="{ checked: item.checked }">{{ item.label }}</span>
        </div>
        <button @click="deleteItem(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [],
      text: "",
    };
  },
  created() {
    this.list = JSON.parse(localStorage.getItem("list")) || [];
  },
  methods: {
    addToList() {
      this.list.unshift({ label: this.text, checked: false });
      localStorage.setItem("list", JSON.stringify(this.list));
      this.text = "";
    },
    deleteItem(indexItem) {
      this.list.splice(indexItem, 1);
      localStorage.setItem("list", JSON.stringify(this.list));
    },
    toggleCheckBox(item) {
      item.checked = !item.checked;
      localStorage.setItem("list", JSON.stringify(this.list));
    },
  },
};
</script>

<style scoped>
.checked {
  text-decoration: line-through;
}
</style>
