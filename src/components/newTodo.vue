<template>
    <form @submit.prevent="addTodo()" action="" class="col-12 col-lf-6">
        <input placeholder="Enter todo" class="form-control" type="text" v-model="newTodo"/>
    </form>
</template>
<script>
export default {
    data(){
        return{
            newTodo:""
        }
    },
    methods:{
        addTodo(){
            if(this.newTodo.length > 1){
                this.$emit('on-addTodo',this.newTodo)
            }
            this.newTodo = "";
        }
    }
}
</script>