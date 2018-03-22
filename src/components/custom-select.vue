<template>
  <div>
    <section>
      <input type="text" v-model="selectedValue.value" :placeholder="selectedValue.value" @click="status = true" readonly>
      <ul v-if="status">
        <li v-for="item in data" :key="item.id"  :class="{selected: item.value === selectedValue.value}" @click="selected(item)">{{item.value}}</li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  name: 'custom-select',
  props: {
    data: {
      type: Array,
      default () {
        return []
      }
    },
    selectedValue: {
      type: Object,
      default () {
        return {}
      }
    }
  },

  created () {
    // 点击其他不在的区域触发事件
    document.querySelector('body').addEventListener('click', this.handleBodyClick)
  },
  destroyed () {
    document.removeEventListener('click', this.handleBodyClick)
  },
  data () {
    return {
      status: false
    }
  },
  methods: {
    selected (data) {
      this.status = false
      this.$emit('receive', data)
    },
    handleBodyClick (e) {
      if (!this.$el.contains(e.target)) {
        this.status = false
      }
    }
  }
}
</script>

<style scoped>
input {
  -webkit-appearance: none;
  background-color: #fff;
  background-image: none;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  border-color: #409eff;
  box-sizing: border-box;
  color: #606266;
  display: inline-block;
  font-size: inherit;
  height: 40px;
  line-height: 40px;
  outline: none;
  padding: 0 15px;
  padding-right: 30px;
  transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
  width: 100%;
  cursor: pointer;
}
ul {
  list-style: none;
  padding: 6px 0;
  margin: 0;
  margin-top: 15px;  
  box-sizing: border-box;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  border-color: #409eff;
}

ul li {
  font-size: 14px;
  padding: 0 20px;
  position: relative;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #606266;
  height: 34px;
  line-height: 34px;
  box-sizing: border-box;
  cursor: pointer;
}

ul .selected {
  color: #409eff;
  font-weight: 700;
}

ul li:hover {
  background-color: #f5f7fa;
}
</style>
