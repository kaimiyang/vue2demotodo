<template>
  <div class="about">
    <h1>Todo 列表</h1>
    <div>
      <button type="button" @click="popAdd">添加</button>
    </div>
    <List :datas="list" 
    @onEdit="handleEditPop"
    @onRemove="handleRemove" />
    <Add v-if="modalAdd" 
    @onAdd="handleAdd" 
    @on-close="handleClose1" />
    <Edit v-if="modalEdit" 
    @onEdit="handleEdit" 
    :item="editItem"
    :index="editIndex"
    @on-close="handleClose2" />
  </div>
</template>

<script>
import { List, Add, Edit } from '../components/todo'
export default {
  components: {
    List,
    Add,
    Edit,
  },
  data() {
    return {
      list: [],
      editIndex: 0,
      editItem: null,
      modalAdd: false,
      modalEdit: false,
    }
  },
  methods: {
    popAdd() {
      this.modalAdd = true
    },
    handleClose1() {
      this.modalAdd = false
    },
    handleClose2() {
      this.modalEdit = false
    },
    handleAdd(item) {
      this.list.push(item)
    },
    handleEdit(item, index) {
      console.log(item, this.list[index])
      // this.list[index] = item
      this.$set(this.list, index, item) //array or object
    },
    handleRemove(index) {
      this.list.splice(index, 1)
    },
    handleEditPop(item, index) {
      this.editItem = item
      this.editIndex = index
      this.modalEdit = true
    },
  }
}
</script>

<style lang="scss" scoped>

</style>
