<template>
    <div>
    <button @click="onClick">Clicked {{counter}} items</button>
    </div>
</template>

<script>
export default {
    name: "Counter",
    data(){
        return{
            counter: 0,
        }
    },
    methods: {
        onClick(){
            this.counter++;
        },
        onMouseOver(){
            console.log('Hovered');
        }
    },

    beforeCreate(){
        this.counter ++;
    },

    created(){
        this.counter = 1;
    },

    beforeMount(){
        console.log('Component root element:', this.$el);
    },

    mounted(){
        const btn = this.$el.querySelector('button');
            if(btn) {
                btn.addEventListener('mouseover', this.onMouseOver);
            }
        console.log(this.$el)
    },

    beforeUpdate(){
        console.log('beforeUpdate');
    },

    updated(){
        console.log('updated');
    },

    beforeDestroy(){
        const btn = this.$el.querySelector('button');
            if(btn) {
                btn.removeEventListener('mouseover', this.onMouseOver);
            }
    },

    destroyed(){
        console.log('destroyed');
    },
}
</script>

<style>

</style>