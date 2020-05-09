<template>
    <div>
        <h1>ToDos</h1>
        <input v-model="newItem" type="text" /><button v-on:click="addItem">Add</button>
        <div>
            <p v-for="(e, index) in myToDos" v-on:click="itemDone(index)" v-bind:key="e">{{ e }}</p>
        </div>
        <div class="listDone">
            <p v-for="(e, index) in myDoneToDos" v-on:click="deleteItem(index)" v-bind:key="e">{{ e }}</p>
        </div>
    </div>
</template>
<script>
    export default {
        name: "todo",
        data(){
            return{
                myToDos: [],
                myDoneToDos: [],
                newItem: ""
            }
        },
        methods:{
            addItem: function () {
                this.myToDos.push(this.newItem)
                this.newItem = ""
            },
            itemDone: function (index) {
                this.myDoneToDos.push(this.myToDos.splice(index, 1)[0])
            },
            deleteItem: function (index) {
                this.myDoneToDos.splice(index,1)
            }

        }

    }
</script>
<style>
    .listDone{
        text-decoration: line-through;
    }
</style>