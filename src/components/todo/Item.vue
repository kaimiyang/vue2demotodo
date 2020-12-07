<template>
  <div class="item">
    <div class="name" :class="[isDone?'done':'do']">{{ item.name }}</div>
    <div class="opt">
      <button type="button" @click="handleEdit">编辑</button>
      <button type="button" @click="handleRemove">删除</button>
    </div>
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
      
    }
  },
  computed: {
    isDone() {
      return this.item.status > 0 ? true : false
    }
  },
  methods: {
    handleEdit() {
      this.$emit('onEdit', this.item, this.index)
    },
    handleRemove() {
      this.$emit('onRemove', this.index)
    }
  }
}
</script>

<style lang="scss" scoped>
.item {
  display: flex;
}
.item>div {
  padding: 5px;
}
.name {

}
.done {
  text-decoration: line-through;
}
.opt {
  display: flex;
}
</style>