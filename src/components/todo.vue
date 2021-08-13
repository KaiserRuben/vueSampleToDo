<template>
  <div class="page-container">
    <div class="todo-container">
      <h1>My ToDos</h1>
      <div class="todo-items-container ">

        <input type="text" class="todo-add" v-model="newItem" @keyup.enter="addItem"/>
        <div class="todo-not-done">
          <p v-for="(e, index) in myToDos" v-on:click="itemDone(index)" v-bind:key="e">{{ e }}</p>
        </div>
        <div class="todo-done">
          <p v-for="(e, index) in myDoneToDos" v-on:click="deleteItem(index)" v-bind:key="e">{{ e }}</p>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "todo",
  data() {
    return {
      myToDos: [],
      myDoneToDos: [],
      newItem: ""
    }
  },
  methods: {
    addItem: function () {
      this.myToDos.push(this.newItem)
      this.newItem = ""
      this.saveChanges()
    },
    itemDone: function (index) {
      this.myDoneToDos.push(this.myToDos.splice(index, 1)[0])
      this.saveChanges()
    },
    deleteItem: function (index) {
      this.myDoneToDos.splice(index, 1)
      this.saveChanges()
    },

    //Not Part of the simple Vue Workshop, for expressJS Workshop
    saveChanges: function () {
      const me = this;
      axios.post('http://localhost:3000/', {
        myToDos: me.myToDos,
        myDoneToDos: me.myDoneToDos
      })
          .then(function (response) {
            console.log(response.data);
          })
          .catch(function (error) {
            console.log(error);
          });
    },
    init: function () {
      const me = this
      axios.get('http://localhost:3000/')
          .then(function (response) {
            me.myDoneToDos = response.data.myDoneToDos
            me.myToDos = response.data.myToDos
          })
          .catch(function (error) {
            console.log(error);
          });
    }

  },
  mounted() {
    // this.init()
  }
  // End of expressJS Workshop part

}
</script>
<style scoped>

body {
  --bg1: #151515;
  --bg2: #252525;
  --done: #6930C3;
  --h1: #64DFDF;
  --p1: #80FFDB;

  background-color: var(--bg1);
  margin: 0;
  padding: 0;
  height: 100vh;
  width: 100vw;

  font-family: "Comfortaa", sans-serif;
}

h1 {
  color: var(--h1);
}

p {
  text-align: center;
}

p:hover {
  cursor: pointer;
}

.page-container {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: center;
}

.todo-container {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: flex-start;

  height: 700px;
  width: 400px;
  max-height: 100vh;
  max-width: 100vw;
  padding: 20px;

  background-color: var(--bg2);

  border-radius: 20px;
}

.todo-items-container {

  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: space-between;

  min-height: 400px;
  width: 400px;
  max-width: 100vw;
  margin-top: 30px;
}

.todo-not-done {
  color: var(--h1);
}

.todo-done {
  color: var(--done);
  text-decoration: line-through;
}

.todo-add {
  width: 80%;
  height: 30px;

  border-radius: 10px;
  border: 0;

  text-align: center;

  color: var(--h1);
  background-color: var(--bg1);

  font-size: 1em;
}

.todo-add:focus {
  outline: none;
  border: 1px solid var(--h1);
}
</style>