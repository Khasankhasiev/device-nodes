<template>
    <div class="container">
        <h1>Device List</h1>
        <DeviceItem
            v-for="(device, index) in devices"
            :key="index"
            :device="device"
            @saveDevice="saveDevice"
            @removeDevice="removeDevice(index)"
        />
        <button @click="addDevice" class="add-button">Add Device</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import DeviceItem from './components/DeviceItem.vue';

const devices = ref([
    {
        name: 'Device 1',
        nodes: [{ name: 'Node 1' }, { name: 'Node 2' }],
        isEditing: false,
    },
]);

const addDevice = () => {
    devices.value.push({ name: 'New Device', nodes: [], isEditing: true });
};

const saveDevice = device => {
    device.isEditing = false;
};

const removeDevice = index => {
    devices.value.splice(index, 1);
};
</script>

<style scoped>
.container {
    max-width: 600px;
    margin: 20px auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
}

h1 {
    text-align: center;
    font-size: 24px;
    margin-bottom: 20px;
}

.add-button {
    display: block;
    margin: 10px auto;
    padding: 10px 20px;
    border: 1px solid #4caf50;
    border-radius: 5px;
    background-color: #4caf50;
    color: white;
    cursor: pointer;
    font-size: 16px;
}

.add-button:hover {
    background-color: #45a049;
}
</style>
