<template>
  <div class="about">
    <h1>Todo 列表</h1>
    <div>
      <button type="button" @click="popAdd">添加</button>
    </div>
    <div><input class="search" type="text" v-model.trim="keyworks" /></div>
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
// import _ from 'lodash'
export default {
  components: {
    List,
    Add,
    Edit,
  },
  data() {
    return {
      list: [],
      listbak: null,
      editIndex: 0,
      editItem: null,
      modalAdd: false,
      modalEdit: false,
      keyworks: ''
    }
  },
  watch: {
    keyworks(val) {
      if (this.listbak === null) {
        this.listbak = this.list
      }
      
      if (val) {
        const result = this.list.filter((item) => {
          const {
            name,
          } = item
          return name.includes(val)
        })
      
        this.list = result
      } else {
        this.list = this.listbak
      }
      
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
.search {
  width: 300px;
  height: 30px;
}
</style>
