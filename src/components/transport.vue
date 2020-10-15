<template>
    <div>
        <h1>Transportt</h1>
        <p v-for="(transport, i) in transports" :key="i" @click="getSelected(transport.category)">{{transport.name}}</p>
    </div>
</template>

<script>
export default {
    name: 'transport',
    data() {
        return {
            choice: '',
            transports: [
                { name: 'ЖП - Гара', category: 'train_station' },
                { name: 'Метро', category: 'subway_station' }, 
                { name: 'Летище', category: 'airport' }, 
                { name: 'Автогара', category: 'bus_station' }
            ],
        }
    },
    methods: {
        getSelected(category) {
            this.$emit('getSelected', category);
        }
    }
}
</script>