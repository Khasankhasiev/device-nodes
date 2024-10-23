<template>
    <li class="node-item">
        <div v-if="node.isEditing" class="editing">
            <input v-model="node.name" class="input" />
            <button @click="$emit('saveNode')" class="save-button">Save</button>
        </div>
        <div v-else class="display">
            <span class="node-name">{{ node.name }}</span>
            <button @click="editNode" class="edit-button">Edit</button>
            <button @click="$emit('removeNode')" class="delete-button">
                Delete
            </button>
            <button
                @click="$emit('moveUp')"
                :disabled="isFirst"
                class="move-up-button"
            >
                Up
            </button>
            <button
                @click="$emit('moveDown')"
                :disabled="isLast"
                class="move-down-button"
            >
                Down
            </button>
        </div>
    </li>
</template>

<script setup>
const props = defineProps({
    node: Object,
    isFirst: Boolean,
    isLast: Boolean,
});

const emit = defineEmits(['saveNode', 'removeNode', 'moveUp', 'moveDown']);

const editNode = () => {
    props.node.isEditing = true;
};
</script>

<style scoped>
.node-item {
    margin-bottom: 10px;
}

.editing {
    display: flex;
    gap: 10px;
    margin-bottom: 5px;
}

.input {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 3px;
}

.save-button {
    background-color: #4caf50;
    border: none;
    color: white;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
}

.save-button:hover {
    background-color: #45a049;
}

.display {
    display: flex;
    gap: 5px;
    align-items: center;
}

.node-name {
    font-size: 16px;
}

.edit-button,
.delete-button,
.move-up-button,
.move-down-button {
    padding: 5px;
    border: none;
    color: white;
    border-radius: 3px;
    cursor: pointer;
}

.edit-button {
    background-color: #ffa500;
}

.edit-button:hover {
    background-color: #e69500;
}

.delete-button {
    background-color: #f44336;
}

.delete-button:hover {
    background-color: #d32f2f;
}

.move-up-button,
.move-down-button {
    background-color: #2196f3;
}

.move-up-button:hover,
.move-down-button:hover {
    background-color: #1e88e5;
}

.move-up-button:disabled,
.move-down-button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}
</style>
