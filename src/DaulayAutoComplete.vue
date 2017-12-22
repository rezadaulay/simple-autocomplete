<template>
    <div class="daulay-autocomplete">
       <input type="text" v-model="keyword" :class="classStyle" :placeholder="placeholder" @keyup="doAction" @blur="doReset">
       <ul v-show="openOptions" class="auto-complete-dropdown-list">
         <li v-for="r in filterResult" :key="r.value" class="options" @mousedown="doSelect(r)">{{r.label}}</li>
       </ul>
    </div>
</template>
<script>
// import Vue from 'vue'

export default {
  props: ['datas', 'classStyle', 'placeholder', 'KeyLabel', 'KeyValue', 'minChars', 'limit', 'parentMethod'],
  data () {
    return {
      keyword: null,
      openOptions: false,
      filterResult: []
    }
  },
  methods: {
    doAction () {
      if (this.keyword.length >= this.minChars) {
        let result = []
        const th_ = this
        this.datas.filter(function (data, index) {
          if (th_.limit > result.length) {
            if (data[th_.KeyLabel].toString().toLowerCase().indexOf(th_.keyword.toLowerCase()) > -1) {
              result.push({value: data[th_.KeyValue], label: data[th_.KeyLabel]})
            }
          }
        })
        if (result.length) {
          this.openOptions = true
          this.filterResult = result
        }
      }
    },
    doReset () {
      this.openOptions = false
    },
    doSelect (data) {
      this.keyword = data.label
      this.parentMethod(data)
    }
  }
}
</script>

<style scoped>
.daulay-autocomplete {
  margin-bottom: 5px;
}
.auto-complete-dropdown-list {
  background: #ecf0f1;
  display: block;
  z-index: 10;
  position: absolute;
  width: 91%;
  margin: 0;
  padding: 0;
}
.auto-complete-dropdown-list .options {
    display: block;
    background-color: #ecf0f1;
    border-bottom: 1px solid #dce4ec;
    color: #000;
    padding: 5px 10px;
    cursor: pointer;
}
.auto-complete-dropdown-list .options:last-child {
    border: 0
}
.auto-complete-dropdown-list .options:hover {
    background-color: #272c40;
    color: #fff;
}
</style>