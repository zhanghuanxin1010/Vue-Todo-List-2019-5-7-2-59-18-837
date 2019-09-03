<template>
 <div id="todoListForm" >
            <input  id="text"  :value="inputingText" @change="handlechange">
            <button @click="handleAdd"  >Add</button>

        </div>
</template>

<script>
export default {
        name: 'createForm',
        data:function(){
           return{
                inputingText:""
           } 

        },
        methods:{
            handleAdd:function(){
                console.log(this.inputingText)
                this.$emit("addNewToDo",this.inputingText)
            },
            handlechange:function(event){
                this.inputingText=event.target.value

            }
        }
}


</script>