<template>
    <li class="d-flex align-items-center list-group-item">
        <button
            v-if="!isEditing"
            :class="{completed}"
            @click="$emit('on-toggle')" 
            class="btn border-0 text-left flex-grow-1"
        >{{todoString}}</button>
        <form v-else @submit.prevent="endEditing()" class="flex-grow-1">
            <input @blur="startEditing()" v-model="newTodoString" type="text" class="form-control"/>
        </form>
        <button @click="startEditing()" class="b btn1">Edit</button>
        <button @click="$emit('on-delete')" class="b btn2">Delete</button>
    </li>
</template>

<script>
export default {
    props: {
        todoString: String,
        completed: Boolean
    },
    data() {
        return {
            isEditing: false,
            newTodoString: ""
        };
    },
    methods: {
        startEditing() {
            if (!this.isEditing) {
                this.newTodoString = this.todoString;
                this.isEditing = true;
            } else {
                this.endEditing();
            }
        },
        endEditing() {
            this.isEditing = false;
            this.$emit("on-edit", this.newTodoString);
        }
    }
};
</script>

<style scoped>
.completed {
    text-decoration: line-through;
}
li{
    background-color: #EAF0F1;
}
.b {
	border-radius:5px;
	border:1px solid #7B8788;
	display:inline-block;
	cursor:pointer;
	color:#fff;
	font-family:Times New Roman;
	font-size:15px;
	font-weight:bold;
	padding:8px 15px;
	text-decoration:none;
}
.btn1:hover {
	background-color: #FAD02E; 
}
.btn2:hover {
	background-color: #ec5b71;
}
.btn1 {
    background-color: #F4C724;
}
.btn2 {
    background-color: #E83350;
}
</style>