<template>
  <div class="add">
    <h2>编辑待办</h2>
    <input class="input" type="text" v-model.trim="editItem" @keyup.enter="handleSubmit" />
    <select v-model="status">
      <option value="0">待办</option>
      <option value="1">已办</option>
    </select>
    <div><button @click="$emit('on-close')">关闭</button></div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      default: () => {}
    },
    index: {
      type: Number,
      default: 0,
    }
  },
  data() {
    return {
      editItem: this.item.name,
      status: this.item.status,
    }
  },
  watch: {
    status(val) {
      console.log(val, this.status)
      this.$emit('onEdit', {
        name: this.editItem,
        status: this.status,
      }, this.index)
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('onEdit', {
        name: this.editItem,
        status: this.status,
      }, this.index)
    }
  }
}
</script>

<style lang="scss" scoped>
.add {
  @include layoutCenter;
  width: 300px;
  height: 150px;
  margin-left: -150px;
  margin-top: -75px;
  background-color: #F5F5F5;
}
.input {
  width: 100%;
  height: 40px;
  font-size: 20px;
}
</style>