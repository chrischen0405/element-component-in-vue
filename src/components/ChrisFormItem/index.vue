<template>
  <div class="form-container">
    <el-form
      ref="formRef"
      :label-width="labelWidth"
      :model="query"
    >
      <el-row>
        <template v-for="(option, index) in formItems">
          <el-col :span="option.colSpan || colSpan" :key="index">
            <el-form-item
              v-if="!option.slot"
              :label="option.label"
              :prop="option.property"
              :style="option.itemStyle || itemStyle"
              size="small"
            >
              <div class="form-item-container">
                <template v-if="option.type === 'input'">
                  <el-input
                    v-model="query[option.property]"
                    :type="option.type"
                    :placeholder="option.placeholder || '请输入'"
                    :disabled="option.disabled || disabled"
                  ></el-input>
                </template>
              </div>
            </el-form-item>
          </el-col>
        </template>
        <el-col
          v-if="isShowControl"
          :span="controlSpan"
          class="btn-container"
        >
          <el-button
            type="primary"
            size="small"
            @click="search"
          >
            搜索
          </el-button>
        </el-col>
      </el-row>
    </el-form>
  </div>
</template>

<script>
export default {
  name: 'ChrisFormItem',
  props: {
    query: {
      type: Object,
      require: true
    },
    formItems: {
      type: Array,
      default: () => []
    },
    labelWidth: {
      type: String,
      default: '110px'
    },
    colSpan: {
      type: Number,
      default: 4
    },
    disabled: {
      type: Boolean,
      default: false
    },
    itemStyle: {
      type: Object,
      default: () => ({ padding: '8px 0px', margin: '0', width: '100%' })
    },
    isShowControl: {
      type: Boolean,
      default: true
    },
    controlSpan: {
      type: Number,
      default: 4
    },
    currentPageName: {
      type: String,
      default: 'currentPage'
    }
  },
  data () {
    return {}
  },
  methods: {
    search () {
      console.log(this.query)
      this.$emit('reload', {
        ...this.query,
        [this.currentPageName]: 1
      }, 'search')
    }
  }
}
</script>

<style scoped lang="scss">
.form-item-container {
  display: flex;
}

.btn-container {
  padding: 8px 0;
  margin: 0 20px;
}
</style>
