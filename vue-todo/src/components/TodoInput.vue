<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter= "addTodo()">
        <span class="addContainer" v-on:click="addTodo()">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
        
        <Modal v-if="showModal" @close="closeModal()">
            <h3 slot="header">
                경고
                <i class="closeModalBtn fas fa-times" v-on:click="closeModal()"></i>
            </h3> 
            <h4 slot="body">입력부탁드립니다.</h4>
        </Modal>
    </div>
</template>

<script>

import Modal from "./common/AlertModal.vue"

export default {
    data(){
        return{
            newTodoItem : "",
            showModal : false
        }    
    },

    methods : {
        addTodo(){
            if (this.newTodoItem !== ""){
                let value = this.newTodoItem && this.newTodoItem.trim();
                let obj = {completed: false, item: value}
                
                //this.$emit("addTodo", obj)
                this.$store.commit("addTodo", obj)

                this.clearInput()
            }else{
                this.showModal = !this.showModal;
            }
        },

        clearInput(){
            this.newTodoItem = ""
        },

        closeModal(){
            this.showModal = false
        }
    },
    components:{
        "Modal" : Modal
    }

    
}
</script>

<style scoped>
    input:focus {
        outline: none;
    }

    .inputBox {
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }

    .inputBox input {
        border-style: none;
        font-size: 0.9rem;
    }

    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    
    .addBtn {
        color: white;
        vertical-align: middle;
    }

    .closeModalBtn{
        color: #42b983;   
    }
</style>
    
