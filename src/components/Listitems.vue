<script>
export default {
    data() {
        return {
            items:[],
        }
    },
    mounted() {
        this.$refs.input.focus()
        if(localStorage.getItem('testlist')) {
            this.items = JSON.parse(localStorage.getItem('testlist'))
        }
    },
    methods: {
        toggle(i) {
            this.items[i].checked = ! this.items[i].checked
        },
        newItem(e) {
            this.items = [...this.items, { text: this.$refs.input.value, checked: false }]
            this.$refs.input.value = ""
            localStorage.setItem('testlist', JSON.stringify(this.items))
        },
        removeItem(item) {
            this.items = this.items.filter((e, i) => (i === item) ? false : true)
            localStorage.setItem('testlist', JSON.stringify(this.items))
        }
    }
}
</script>

<template>
    <div>
        <ul>
            <li v-for="item in items">
                <input type="checkbox" @click="toggle" v-model="item.checked">
                {{ item.text }}
                <div @click="removeItem(items.indexOf(item))" class="remove">x</div>
            </li>
        </ul>
        <div class="input">
            <input ref="input" type="text" @keyup.enter="newItem">
        </div>
    </div>
</template>

<style scoped>
.remove {
    color: red;
    display: inline-block;
    padding-left: 25px;
}
</style>