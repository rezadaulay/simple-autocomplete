<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Simple Vue Apps</h1>
    <h2>Autocomplete With Local Array</h2>
    <DaulayAutoComplete placeholder="Search Technician" :datas="lists" KeyLabel="name" KeyValue="id" minChars="1" limit="15" classStyle="form-control input-sm" :parentMethod="doFilter" />
  </div>
</template>

<script>
import DaulayAutoComplete from './components/DaulayAutoComplete'
export default {
  name: 'app',
  components: {
    DaulayAutoComplete
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      lists: [
        {id: 1, name: 'Muhammad'},
        {id: 2, name: 'Isa'},
        {id: 3, name: 'Yusuf'},
        {id: 4, name: 'Ibrahim'},
        {id: 5, name: 'Aldi'},
        {id: 6, name: 'Tahir'},
        {id: 7, name: 'Aidil Sinaga'},
        {id: 8, name: 'Hutahean Sinambela'},
        {id: 9, name: 'Joko'},
        {id: 10, name: 'Abu'}
      ]
    }
  },
  methods: {
    doFilter (data) {
      const th_ = this
      this.lists.filter((list, index) => {
        if (data.value === list.id) {
          console.log('You selected : ' + list.name)
        }
      })
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
