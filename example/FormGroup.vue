<template>
  <el-card
    class="demo-card"
    header="ele-form-group 简单示例"
    shadow="never"
  >
    <div class="form-desc-group">
      <div style="width: 600px">
        <ele-form-group
          :formData="formData"
          :groups="groups"
          :request-fn="handleSubmit"
          @request-success="handleSuccess"
        />
      </div>
      <div style="margin-left: 50px;width: 500px;">
        <codemirror
          @input="handleCodeChange"
          v-model="code"
        />
      </div>
    </div>
  </el-card>
</template>

<script>
export default {
  inject: ['checkType'],
  data () {
    return {
      groups: [],
      code:
        `[
  {
    // groupId 为分组的 id
    groupId: 'base',
    // groupLabel 为分组的 label
    groupLabel: '基础信息',
    // form 为分组的 ele-form 属性
    form: {
      // 该分组的 ele-form 属性中的 form-desc
      formDesc: {
        name: {
          type: 'input',
          label: '姓名'
        },
        age: {
          type: 'number',
          label: '年龄'
        }
      },
      // 该分组中 ele-form 属性中 form-data
      formData: {
        name: 'zhang'
      },
      // 会覆盖 ele-form-group 中定义的 submitBtnText
      submitBtnText: '发起'
    },
    // on 为分组的事件
    on: {
      // 会覆盖 ele-form-group中定义的 @request, 实现定制化
      request (data) {
        console.log('点击的第一个', data)
      }
    }
  },
  {
    groupId: 'password',
    groupLabel: '密码',
    form: {
      formDesc: {
        oldPassword: {
          type: 'password',
          label: '旧密码'
        },
        newPassword: {
          type: 'password',
          label: '新密码'
        },
        confirmPassword: {
          type: 'password',
          label: '确认密码'
        }
      },
      formData: {
        oldPassword: '123'
      }
    }
  }
]
`,
      formData: {}
    }
  },
  methods: {
    handleSubmit (data) {
      /* eslint-disable */
      console.log(data)
      return Promise.resolve()
    },
    handleSuccess () {
      this.$message.success('创建成功')
    },
    handleCodeChange (code) {
      try {
        /* eslint-disable */
        const codeData = eval('(' + code + ')')
        this.groups = codeData
      } catch { }
    }
  },
  created () {
    this.handleCodeChange(this.code)
  }
}
</script>

<style>
.form-desc-group {
  display: flex;
  justify-content: center;
}
.form-desc-group .CodeMirror {
  height: 500px !important;
}
</style>
