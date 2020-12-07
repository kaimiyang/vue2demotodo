<template>
  <div class="lay">
    <Item v-for="(item,i) in datas" :key="i"
    :item="item" :index="i"
    @onEdit="handleEdit"
    @onRemove="handleRemove"
    />
  </div>
</template>

<script>
import Item from './Item'
export default {
  props: {
    datas: {
      type: Array,
      default: () => []
    }
  },
  components: {
    Item,
  },
  methods: {
    handleEdit(item, index) {
      this.$emit('onEdit', item, index)
    },
    handleRemove(index) {
      this.$emit('onRemove', index)
    }
  }
}
</script>

<style lang="scss" scoped>
.lay {
  @include flexCenter;
  flex-flow: column nowrap;
}
</style>