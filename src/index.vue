<template>
  <div class="component">
    <div class="v-badge">
      <slot class="badge-slot" name="slot0"></slot>
      <!--<span class="badge-slot">数据查询</span>-->
      <sup
        class="v-badge__content is-fixed"
        :class="['v-badge__content--' + this.bType, isDot ? 'is-dot':'']">{{info&&info[0]&&!isDot?info[0]:''}}</sup>
    </div>
  </div>
</template>

<script>
  import {VueExtend} from 'godspen-lib'

  export default {
    mixins: [VueExtend.mixin],
    name: 'v-badge',
    label: process.env.LABEL,
    style: process.env.STYLE,
    stack: false, // 是否是堆叠模式 ，true：孩子元素会按楼层一个个向下排布， false: 孩子元素绝对定位，随意放置位置
    childLimit: 9999,  // 孩子元素最大限制数
    leaf: false, // 是否是叶子节点，为true的时候该节点下面不能添加节点
    props: {
      datasourcekey: {
        type: String,
        default: '',
        editor: {
          ignore: true
        }
      },
      data: {
        type: Array,
        default () {
          return ['hot']
        },
        editor: {
          ignore: true
        }
      },
      isDot: {
        type: Boolean,
        default: true,
        editor: {
          label: '小红点',
          desc: '不展示数字，只有一个小红点'
        }
      },
      bType: {
        type: String,
        editor: {
          type: 'enum',
          label: '类型',
          desc: '徽标背景色',
          defaultList: [
            'primary',
            'success',
            'warning',
            'danger',
            'info'
          ]
        },
        default: ''
      }
    },
    computed: {
      info () {
        var data = this.data
        if (this.datasourcekey) {
          var dataStr = this.dataHubGet && this.dataHubGet(this.datasourcekey)
          try {
            data = JSON.parse(dataStr)
          } catch (e) {
            console.log('error v-badge', '获取数据解析json对象异常')
            data = []
          }
        }
        return data
      }
    },
    editorMethods: {
    },
    methods: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component {
    position: relative;
    vertical-align: middle;
    display: inline-flex;

    .v-badge {
      position: relative;
      vertical-align: middle;
      line-height: 1;
      display: inline-block;

      .v-badge__content {
        background-color: #f56c6c;
        border-radius: 10px;
        color: #fff;
        display: inline-block;
        font-size: 12px;
        height: 18px;
        line-height: 18px;
        padding: 0 6px;
        text-align: center;
        white-space: nowrap;
        border: 1px solid #fff;
        &.is-fixed {
          position: absolute;
          top: 0;
          right: 10px;
          transform: translateY(-50%) translateX(100%);
        }
        &.is-fixed.is-dot {
          height: 8px;
          width: 8px;
          padding: 0;
          right: 5px!important;
          border-radius: 50%;
        }
        &.is-fixed.is-corner{
          width: 40px;
          position: absolute;
          right: -32px;
          top: 8px;
          white-space: nowrap;
          transform: rotate(45deg);
          text-align: center;
          font-size: 15px;
        }
      }

      .v-badge__content--primary {
        background-color: #409eff;
      }
      .v-badge__content--success {
        background-color: #67C23A;
      }
      .v-badge__content--warning {
        background-color: #e6a23c;
      }
      .v-badge__content--danger {
        background-color: #F56C6C;
      }
      .v-badge__content--info {
        background-color: #909399s;
      }
    }
  }
</style>
