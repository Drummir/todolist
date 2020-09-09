<template>
  <div class="tasks">
    <table class="tableClass">
      <thead>
        <tr>
          <th scope="col">Задачи:</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="item.id">
          <th scope="row">
            <div class="taskRow">
              <div class="task-info" :class="{completed: item.completed}">
                <input type="checkbox" :id="`check${index}`" v-model="item.completed" @change="changeTaskState()" />
                <label :for="`check${index}`">{{ item.title }}</label>
              </div>
              <div class="task-btn">
                <button @click="deleteItem(index)" class="btnDel">x</button>
              </div>
            </div>
          </th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  props: ['items'], // Входящие данные
  
  methods: {
    deleteItem: function(index) {
      this.$emit("deleteTask", index)
    },
    changeTaskState() {
      this.$store.commit('setItems', this.items);
    }
  }
}
</script>

<style>
.tasks {
  @border: 1px solid red;
  display: flex;
  justify-content: center;
}

.tableClass {
  border: 1px solid red;
  font-size: 24px;
  font-family: Consolas;
  height: 100%;
}

th {
  min-width: 425px;
  max-width: 425px;
}

.taskRow {
  background: #dcdcdc;
  display: flex;
  justify-content: flex-start;
  flex-direction: row;
  height: 100%;
}

.task-info {
  flex-basis: 90%;
  text-align: left;
  padding-left: 10px;
  padding-top: 5px;
  padding-bottom: 5px;
}

.task-info.completed {
	text-decoration: line-through;
}

input[type=checkbox] {display: none;}

input[type=checkbox] + label:before {
    content: "\2714";
    color: transparent;
    display: inline-block;
    border: 1px solid #ccc;
    font-size: 20px;
    font-weight: 900;
    line-height: 22px;
    margin: -5px 5px 0 0;
    height: 20px;
    width: 20px;
    text-align: center;
    vertical-align: middle;
    transition: color ease .3s;
}

input[type=checkbox]:checked + label:before {
  color: #4CAF50;
  border-color: #000;
}

input[type=checkbox]:hover + label:before {
  border: 1px solid #4CAF50;
}

.task-btn {
  display: flex;
  align-items: center;
  height: 100%;
}

.btnDel {
    background-color: #cc1b2e; /* Green */
    border: none;
    border-radius: 3px;
    color: white;
    padding: 5px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
}

</style>