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
    import axios from 'axios'
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
                this.saveChanges()
            },
            itemDone: function (index) {
                this.myDoneToDos.push(this.myToDos.splice(index, 1)[0])
                this.saveChanges()
            },
            deleteItem: function (index) {
                this.myDoneToDos.splice(index,1)
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
            this.init()
        }
        // End of expressJS Workshop part

    }
</script>
<style>
    .listDone{
        text-decoration: line-through;
    }
</style>