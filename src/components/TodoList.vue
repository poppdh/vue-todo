<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
                <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
                <span v-bind:class="{checkBtnCompleted: todoItem.completed}">{{ todoItem.item }}</span>
                <span class="removeBtn"><i class="fas fa-trash-alt" v-on:click="removeTodo(todoItem, index)"></i></span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data: function(){
        return{
            todoItems: []
        }
    },
    methods:{
        removeTodo: function(todoItem, index){
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
            localStorage.removeItem(todoItem.item);
        },
        toggleComplete: function(todoItem, index){
            localStorage.removeItem(todoItem.item);
            todoItem.completed = !todoItem.completed;
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        }
    },
    created: function(){
        if(localStorage.length > 0){
            for(var i = 0; i < localStorage.length; i++){
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    //console.log(localStorage.getItem(localStorage.key(i)))
                    console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                }
            }
        }
    }
}
</script>

<style>
ul{
    list-style-type: none;
    padding-left: 0;
    margin-top: 0;
    text-align: left;
}
li{
    display: flex;
    min-width: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background-color: #ffffff;
    border-radius: 5px;
}
.checkBtn{
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}
.checkBtnCompleted{
    text-decoration: line-through;
    color: #b3adad;
}
.removeBtn{
    margin-left: auto;
    color: #de4343;
}
</style>
