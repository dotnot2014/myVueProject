<template>
  <div id="app">
    <h1 v-html="title"></h1>
    <input v-model="newitem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :class="{finished: item.isFinish}" @click="toggleFinish(item)">
          {{ item.label }}
      </li>
    </ul>
    <component-A msgfromfather="god bless you!" v-on:childsay="tellsomething"></component-A>
    <p>the boy say: {{ childwords }}</p>
  </div>
</template>

<script>
import Store from './store'
import componentA from './components/componentA'

export default {
  data(){
    return{
      title: "<span>#</span>this is a todolist",
      items: Store.fetch(),
      newitem:"",
      childwords:""
    }
  },
  components: { componentA },
  watch: {
    'items': {
          handler: function (items) { 
            Store.save(items)
          },
          deep: true
        }
  },
  methods: {
      toggleFinish: function(item){
          item.isFinish = !item.isFinish;
      },
      addNew: function(){
        this.items.push({
          label: this.newitem,
          isFinish: false
        });
        this.newitem='';
      },
      tellsomething: function(msg){
          this.childwords = msg;
      }
  }
}
</script>

<style>
.finished{
  text-decoration : line-through;
}

html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
