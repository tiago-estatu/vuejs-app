<template>
    <div>
        <form v-on:submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo item...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
// Creates a ID key em tempo de execução
//import uuid from 'uuid';

    export default {
        name:"AddTodo",
        data(){
            return {
                title: ''
            }
        },
        methods: {
            addTodo(e){
                e.preventDefault();

                const newTodo = {
                    //id: uuid.v4(),
                    title: this.title,
                    completed: false
                }
                // Enviar para o (Parent)
                this.$emit('add-todo', newTodo)

                // Limpar o campo text
                this.title = '';
            }
        }      
    }
</script>

<style scoped>
    form {
        display: flex
    }
    input[type="text"] {
        flex:10;
        padding: 5px;
    }
    input[type="submit"] {
        flex:2;
    }
</style>