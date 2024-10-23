<template>
    <div class="device-item">
        <div v-if="device.isEditing" class="editing">
            <input v-model="device.name" class="input" />
            <button @click="onSaveDevice" class="save-button">Save</button>
        </div>
        <div v-else class="display">
            <span class="device-name">{{ device.name }}</span>
            <button @click="editDevice" class="edit-button">Edit</button>
            <button @click="$emit('removeDevice')" class="delete-button">
                Delete
            </button>
        </div>
        <ul class="node-list">
            <NodeItem
                v-for="(node, nodeIndex) in device.nodes"
                :key="nodeIndex"
                :node="node"
                @saveNode="saveNode(node)"
                @removeNode="removeNode(nodeIndex)"
                @moveUp="moveNodeUp(nodeIndex)"
                @moveDown="moveNodeDown(nodeIndex)"
                :isFirst="nodeIndex === 0"
                :isLast="nodeIndex === device.nodes.length - 1"
            />
        </ul>
        <button @click="addNode" class="add-node-button">Add Node</button>
    </div>
</template>

<script setup>
import NodeItem from './NodeItem.vue';

const props = defineProps({
    device: Object,
});

const emit = defineEmits(['saveDevice', 'removeDevice']);

const editDevice = () => {
    props.device.isEditing = true;
};

const onSaveDevice = () => {
    emit('saveDevice', props.device);
};

const addNode = () => {
    props.device.nodes.push({ name: 'New Node', isEditing: true });
};

const saveNode = node => {
    node.isEditing = false;
};

const removeNode = index => {
    props.device.nodes.splice(index, 1);
};

const moveNodeUp = index => {
    if (index > 0) {
        const temp = props.device.nodes[index];
        props.device.nodes[index] = props.device.nodes[index - 1];
        props.device.nodes[index - 1] = temp;
    }
};

const moveNodeDown = index => {
    if (index < props.device.nodes.length - 1) {
        const temp = props.device.nodes[index];
        props.device.nodes[index] = props.device.nodes[index + 1];
        props.device.nodes[index + 1] = temp;
    }
};
</script>

<style scoped>
.device-item {
    padding: 15px;
    margin-bottom: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
    background-color: #fff;
}

.editing {
    display: flex;
    gap: 10px;
    margin-bottom: 10px;
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
    justify-content: space-between;
    align-items: center;
}

.device-name {
    font-size: 18px;
}

.edit-button {
    background-color: #ffa500;
    border: none;
    color: white;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
}

.edit-button:hover {
    background-color: #e69500;
}

.delete-button {
    background-color: #f44336;
    border: none;
    color: white;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
}

.delete-button:hover {
    background-color: #d32f2f;
}

.node-list {
    margin-top: 10px;
    padding-left: 20px;
}

.add-node-button {
    margin-top: 10px;
    padding: 5px 10px;
    background-color: #2196f3;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}

.add-node-button:hover {
    background-color: #1e88e5;
}
</style>
