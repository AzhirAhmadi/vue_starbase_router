<template>
    <div class="col-md-12">
        <div class="row">
            <Item 
                v-for="(item, index) in items"
                :key="index"
                :passed-item="item"
                :type="type"
                />
        </div>
    </div>
</template>

<script>
import Item from './Item.vue'
export default {
    data() {
        return {
            type: this.$route.params.type,
            items: []
        }
    },
    watch: {
        '$route': 'fetchItems'
    },
    methods: {
        fetchItems() {
            this.items = []
            let initial_ids = [1, 13, 14]
            this.type = this.$route.params.type

            for (let i in initial_ids) {
                let id = initial_ids[i]
                fetch(`https://swapi.co/api/${this.type}/${id}/`,{
                method: 'GET'
                }).then(response => response.json())
                .then(json => this.items.push(json))
            }
        }
    },
    created() {
        this.fetchItems()
    },
    components:{
        Item
    }
}
</script>