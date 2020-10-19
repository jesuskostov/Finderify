<template>
    <div class="w-100">
        <h3 class="mt-3 mb-4">Транспорт</h3>
        <div class="type-container">
            <p v-for="(type, i) in data" :key="i" @click="getSelected(type.category)" class="types" :class="{active: choice == type.category}">{{type.name}}</p>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.type-container {
    width: 100%;
    text-align: center;

    .types {
        cursor: pointer;
        padding: 10px;
        margin-right: 8px;
        display: inline-block;
        color: #fff;
        background-color: rgba(147, 39, 180, 0.6);
        border-radius: 999999px;

        &.active {
            background-color: rgba(147, 39, 180, 1);
        }
    }
}
@media (max-width: 768px) {
    .type-container {
      display: flex;
      overflow-x: scroll;
      padding: 0 15px;

      .types {
          flex-shrink: 0;
      }
    }
}
</style>

<script>
export default {
    name: 'transport',
    props: ['info', 'reset'],
    data() {
        return {
            choice: '',
            data: null,
        }
    },
    methods: {
        getSelected(category) {
            this.$emit('getSelected', category);
            this.choice = category
        }
    },
    created() {
        if(this.info == 'transport') {
            this.data = [
                { name: 'ЖП - Гара', category: 'train_station' },
                { name: 'Метро', category: 'subway_station' }, 
                { name: 'Летище', category: 'airport' }, 
                { name: 'Автогара', category: 'bus_station' }
            ]
        } else if (this.info == 'service') {
            this.data = [
                {name: 'Банкомати', category: 'atm'},
                {name: 'Банки', category: 'bank'},
                {name: 'Пекарни', category: 'bakery'},
                {name: 'Доктори', category: 'doctor'},
                {name: 'Зъболекари', category: 'dentist'},
                {name: 'Автокъщи', category: 'car_dealer'},
                {name: 'Сервизи', category: 'car_repair'},
                {name: 'Автомивки', category: 'car_wash'},
                {name: 'Адвокати', category: 'lawyer'},
                {name: 'Бояджии', category: 'painter'},
                {name: 'Паркинги', category: 'parking'},
                {name: 'Ветеринари', category: 'veterinary_care'},
                {name: 'Бензиностанции', category: 'gas_station'},
                {name: 'Аптеки', category: 'pharmacy'},
                {name: 'Пощи', category: 'post_office'},
            ]
        } else if (this.info == 'entertainment') {
            this.data = [
                {name: 'Барове', category: 'bar'},
                {name: 'Кафета', category: 'cafe'},
                {name: 'Казина', category: 'casino'},
                {name: 'Нощни клубове', category: 'night_clubs'},
                {name: 'Паркове', category: 'park'},
                {name: 'Спа', category: 'spa'},
                {name: 'Боулинг', category: 'bowling_alley'},
                {name: 'Ресторанти', category: 'restaurant'},
                {name: 'Молове', category: 'shopping_mall'},
            ]
        } else if (this.info == 'care') {
            this.data = [
                {name: 'Фитнес', category: 'gym'},
                {name: 'Салони за красота', category: 'beauty_salon'},
                {name: 'Фризьорски салони', category: 'hair_care'},
            ]
        }
    }
}
</script>
