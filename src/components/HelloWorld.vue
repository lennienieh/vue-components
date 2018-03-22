<template>
  <div class="hello">
    {{getData}}
    <custom-select :data="list" :selected-value="getData"  class="select" @receive="getValueHandle"></custom-select>
  </div>
</template>

<script>
import customSelect from '@/components/custom-select'
export default {
  name: 'HelloWorld',

  components: {
    customSelect
  },

  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      list: [
        { id: 1, value: '1' },
        { id: 2, value: '2' },
        { id: 3, value: '3' },
        { id: 4, value: '4' }
      ],
      getData: {
        id: 1,
        value: '1'
      }
    }
  },

  methods: {
    getValueHandle (value) {
      this.getData = value
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.select {
  width: 300px;
  margin: 0 auto;
}
</style>
