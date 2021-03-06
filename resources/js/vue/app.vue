<template>
  <div class="todoListContainer">
    <div class="heading">
      <h2 id="title">Todo List</h2>
      <add-item-form @reloadList="getItems()"/>
    </div>
    <list-view :items="items" @reloadList="getItems()"/>
  </div>
</template>

<script>
import AddItemForm from './AddItemForm'
import ListView from './ListView'

export default {
  data() {
    return {
      items: []
    }
  },
  components: {
    AddItemForm,
    ListView
  },
  methods: {
    getItems() {
      axios.get('api/items')
      .then(res => {
        console.log(res)
        this.items = res.data
      })
      .catch(error => console.log(error))
    }
  },
  created() {
    this.getItems()
  }

}
</script>


<style scoped>
.todoListContainer {
  width: 350px;
  margin: auto;
}
.heading {
  background: #e6e6e6;
  padding: 10px;
}
#title {
  text-align: center;
}
</style>
