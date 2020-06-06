<template>
  <div class="component-editor">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>徽标数据</span>
      </div>
      <el-form ref="form" label-width="60px" size="mini">
        <el-form-item label="使用数据源:" label-width="100px">
          <el-checkbox border size="mini" v-model="usedatasource"></el-checkbox>
        </el-form-item>
      </el-form>
      <el-form v-if="usedatasource" ref="form" label-width="60px" size="mini">
        <el-form-item label="数据源:" label-width="100px">
          <el-input placeholder="填写数据总线的key" v-model="componentInfo.datasourcekey"></el-input>
        </el-form-item>
      </el-form>
      <el-form v-else ref="form" label-width="60px" size="mini">
        <el-form-item label="显示值:">
          <el-tooltip class="item" effect="dark" content="展示的数字或文案" placement="top" slot="label">
            <span>显示值:</span>
          </el-tooltip>
          <el-input placeholder="展示的数字或文案" v-model="componentInfo.data[0]"></el-input>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
  export default {
    name: 'maliangeditor',
    props: {
      // 编辑器会传递给编辑面板组件的属性值，编辑器可以修改这些值来达到控制组件数据的作用
      componentInfo: { // 固定字段，收集所有属性值
        type: [Object],
        default () {
          return {
            rdatasourcekey: '',
            data: ['hot']
          }
        }
      }
    },
    data: function () {
      return {
        usedatasource: false,
      }
    },
    computed: {
    },
    watch: {
      'componentInfo.data': {
        handler (v) {
          console.log(v)
        },
        deep: true
      }
    },
    mounted: function () {
    },
    methods: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component-editor {
  }
</style>
