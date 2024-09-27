<template>
    <div class="todo-item">
        <p><strong>{{ identifier }}:</strong> {{ title }} - {{ description }}</p>
        <button @click="editTask">Edit</button>
        <button @click="deleteTask">Delete</button>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: {
        identifier: String,
        title: String,
        description: String
    },
    methods: {
        editTask() {
            this.$emit('edit-task', this.identifier);
        },
        deleteTask() {
            this.$emit('delete-task', this.identifier);
        }
    },
    created() {
        console.log('TodoItem component created with ID:', this.identifier);
    }
}
</script>
<style scoped>
.todo-item {
    display: flex;
    justify-content: space-between;
    margin: 10px 0;
    padding: 10px;
    background-color: #f5f5f5;
    border-radius: 5px;
}

button {
    background-color: #6c63ff;
    color: white;
    border: none;
    border-radius: 3px;
    padding: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #4b47db;
}
</style>
