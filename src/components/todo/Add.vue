<template>
  <div class="add">
    <h2>添加待办</h2>
    <input class="input" type="text" v-model.trim="addItem" @keyup.enter="handleSubmit" />
    <button @click="$emit('on-close')">关闭</button>
  </div>
</template>

<script>
export default {
  props: {
    index: {
      type: Number,
      default: 0,
    }
  },
  data() {
    return {
      addItem: '',
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('onAdd', {
        name: this.addItem,
        status: 0,
      })
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