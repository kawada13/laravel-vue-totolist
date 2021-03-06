<template>
  <div>
    <input 
      type="checkbox"
      @change="updateCheck()"
      v-model="item.completed"
    >
    <span :class="[item.completed ? 'completed' : '', 'itemText']">{{item.name}}</span>
    <button @click="removeItem()" class="trashcan">
      <font-awesome-icon icon="trash"/>
    </button>
  </div>
</template>

<script>
export default {
  props: ['item'],
  methods: {
    updateCheck() {
      axios.put(`api/item/${this.item.id}`, {
        item: this.item
      })
      .then(res => {
        console.log(res);
        if(res.status == 200) {
          this.$emit('itemchanged')
        }
      })
      .catch(erroe => console.log(error))
    },
    removeItem() {
      axios.delete(`api/item/${this.item.id}`)
      .then(res => {
        console.log(res);
        if(res.status == 200) {
          this.$emit('itemchanged')
        }
      })
      .catch(erroe => console.log(error))
    },
  }

}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: brown;
}
.itemText {
  width: 100%;
  margin-left: 20px;
  align-items: center;
}
.trashcan {
  background: #e6e6e6;
  border: none;
  color: #FF0000;
  outline: none;
}
</style>