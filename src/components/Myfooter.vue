<template>
        <div class="todo-footer" v-show="total">
      <label>
          <!-- 全选的第一种做法 -->
          <!-- <input type="checkbox" :checked="isAll" @change="checkAll" /> -->
          <!-- 全选的第二种做法 -->
          <input type="checkbox" v-model="isAll"/>
      </label>
      <span>
          <span>已完成{{doneTotal}}</span>  /  全部{{total}}
      </span>
      <button class="btn btn-danger" @click="clearAll">清楚已完成任务</button>

    </div>
</template>

<script>
export default {
    name:'Myfooter',
    props:["todos","checkAllTodo","clearnAllTodo"],
    computed:{
        total(){4
            return this.todos.length
        },
        doneTotal(){
            return this.todos.reduce((pre,cursor)=>pre+(cursor.done ? 1:0),0)
        },
        isAll:{
            // return this.doneTotal === this.total && this.total >0
            get(){
                return this.doneTotal === this.total && this.total >0
            },
            set(value){
                this.checkAllTodo(value)
            }
        }
    },
    methods: {
        checkAll(e){
            this.checkAllTodo(e.target.checked)
        },
        clearAll(){
            this.clearnAllTodo()
        }
    },
}
</script>

<style scoped>
 
/* footer */
.todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
}                                   
.todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
}
.todo-footer label input{
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
}
.todo-footer button{
    float: right;
    margin-top: 5px;
}
</style>