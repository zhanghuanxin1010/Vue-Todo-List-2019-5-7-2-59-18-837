
<template>
  <div id="app">
    <h2>
      Vue To Do List
      Simple Todo List with adding and filter by diff status.
    </h2>
    <div id="todoListForm">
      <input id="text" v-model="inputingText" />
      <button @click="handleAdd">Add</button>
    </div>

    <div id="list">
      <ul>
        <li v-for="(item,index) in filterTodoList" :key="index" @click="handleEvent(index)">
          <input type="checkbox" />        
          {{item.content}}
        </li>
      </ul>
    </div>
    <div>
      当前状态
      <button @click="handleStatus('active')">active</button>

      <button @click="handleStatus('complete')">complete</button>
      <!-- <createForm @addNewToDo="addNewToDo"></createForm> -->
    </div>
  </div>
</template>

<script>
import createForm from "./components/createForm.vue";
export default {
  name: "app",
  components: {
    createForm
  },
  data: function() {
    return {
      /**
       * 定义了 todo item 中属性为 {content:'吃饭',status:'active'}
       * 定义了 todo 的两种状态 completed、active，默认为 active
       */
    //   todoList: [
    //     { content: "吃饭", status: "active" ,choosed:false},
    //     { content: "写作业", status: "active" ,choosed:false}
    //   ],
      currrentFilter: "active",
      inputingText: ""
    };
  },
  computed: {
    getCurrStatus: function() {
        return (index)=>  this.$store.state.todoList[index].status == 'active';
    },
    filterTodoList: function() {
      let filterList = [];
      for (let index = 0; index <  this.$store.state.todoList.length; index++) {
        const element =  this.$store.state.todoList[index];
        if (element.status == this.currrentFilter) {
          filterList.push(element);
        }
      }
      return filterList;
    }
  },

  methods: {
    handleInput:function(event) {
        console.log(event);
    },
    handleAdd: function() {
      console.log(this.inputingText);
      this.todoList.push({
        content: this.inputingText,
        status: "active"
      });

      this.inputingText = "";
      console.log( this.$store.state.todoList);
    },
    handleStatus: function(status) {
      this.currrentFilter = status;
    },
    addNewToDo: function(inputingText) {
      console.log(this.inputingText);
      this.todoList.push({
        content: inputingText,
        status: "active"
      });
    },
    handleEvent: function(index) {

    //   console.log(this.todoList[index].status);
       this.$store.state.todoList[index].status = "complete";
      console.log( this.$store.state.todoList);
    }

    // handleActive:function(){
    //     this.currrentFilter='active';
    // },
    // handleComplete:function(){
    //     this.currrentFilter='complete';
    // }
  },
  watch : {
      "todoList" : function(newVal,oldVal) {
          console.log(newVal);
      }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.items {
  list-style: none;
  text-align: left;
  line-height: 30px;
}

.items li.completed {
  text-decoration: line-through;
}

.filter a {
  margin: 0 10px;
  line-height: 30px;
}

.filter a.active {
  color: #f60;
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: 3px;
  cursor: pointer;
}
</style>
