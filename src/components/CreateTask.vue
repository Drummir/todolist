<template>

    <div class="form-group">
      <div class="input-group">
        <input  type="text" 
                placeholder="Поставь себе цель"
                v-model="taskMessage" 
        />
        <div class="input-btn">
          <button class="btnAdd" @click="addItem">Добавить</button>
        </div>    
      </div>
    </div>

</template>

<script>
export default {
    props: ['items'], // Входящие данные

    data() {
      return {
        taskMessage: ''
      }
    },

    methods: {
    addItem: function () {
      if(this.taskMessage !== '') {
        this.items.unshift({
          title: this.taskMessage,
          completed: false
        });
       this.taskMessage = '';
      }
    },
  },
}
</script>

<style>
.form-group {
 @display: inline-block;
 @border: 1px solid red;
}

.input-group {
  @border: 1px solid blue;
  @display: inline-block;
  display: flex;
  justify-content: center;
  flex-direction: row;
  height: 100%;
}

input {
  font-size: 24px;
  border: 1px solid #adadad;
  border-radius: 2px;
}

input::placeholder {
  color: #adadad;
  font-family: Consolas;
  font-style: italic;
}

.input-btn {
  @border: 1px solid green;
}

.btnAdd {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
}
</style>