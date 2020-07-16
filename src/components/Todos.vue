<template>
    <div>
        <h3>Todos</h3>
        <div class="todos">
            <div v-for="todo in allTodos" :key="todo.id" class="todo" :class="{'is-complete':todo.completed}"
                 @dblclick="onDblClick(todo)">
                <p>
                    {{ todo.title }}
                </p>
                <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
            </div>
        </div>
    </div>
</template>

<script>
    import {mapGetters, mapActions} from 'vuex';

    export default {
        name: "Todos",
        methods: {
            ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
            onDblClick(todo) {
                const updTodo = {
                    id: todo.id,
                    title: todo.title,
                    completed: !todo.completed
                };
                this.updateTodo(updTodo);
            },
        },
        computed: mapGetters(['allTodos']),
        created() {
            this.fetchTodos();
        }
    }
</script>

<style scoped>

    p { /* To avoid selecting the text on double click */
        -webkit-user-select: none; /* Chrome/Safari */
        -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* IE10+ */
    }

    .todos {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 1rem;
    }

    .todo {
        border: 1px solid #ccc;
        background: #42b983;
        padding: 1rem;
        border-radius: 5px;
        text-align: center;
        position: relative;
        cursor: pointer;
    }

    i {
        position: absolute;
        bottom: 10px;
        right: 10px;
        color: #ffffff;
        cursor: pointer;
    }

    .is-complete {
        text-decoration: line-through;
    }

    @media (max-width: 500px) {
        .todos {
            grid-template-columns: 1fr;
        }
    }
</style>