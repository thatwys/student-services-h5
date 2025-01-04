<template>
  <div class="container">
    <header>
      <h1>告诉我们您的需求</h1>
      <p class="subtitle">全方位服务、轻松解决</p>
    </header>

    <a-form
      :model="formState"
      @finish="onFinish"
      layout="vertical"
    >
      <a-form-item
        label="需求类型"
        name="demandType"
        :rules="[{ required: true, message: '请选择需求类型' }]"
      >
        <a-select
          v-model:value="formState.demandType"
          @change="handleTypeChange"
          placeholder="请选择需求类型"
        >
          <a-select-option value="租房服务">租房服务</a-select-option>
          <a-select-option value="搬家服务">搬家服务</a-select-option>
          <a-select-option value="学业辅导">学业辅导</a-select-option>
          <a-select-option value="求职辅导">求职辅导</a-select-option>
          <a-select-option value="other">其他</a-select-option>
        </a-select>
      </a-form-item>

      <a-form-item
        v-if="showOther"
        name="otherType"
        :rules="[{ required: true, message: '请输入需求类型' }]"
      >
        <a-input
          v-model:value="formState.otherType"
          placeholder="请输入需求类型"
        />
      </a-form-item>

      <a-form-item
        label="预期时间"
        name="expectedDate"
        :rules="[{ required: true, message: '请选择预期时间' }]"
      >
        <a-date-picker
          v-model:value="formState.expectedDate"
          style="width: 100%"
        />
      </a-form-item>

      <a-form-item
        label="需求描述"
        name="description"
        :rules="[{ required: true, message: '请输入需求描述' }]"
      >
        <a-textarea
          v-model:value="formState.description"
          :rows="4"
          placeholder="请详细描述您的需求..."
        />
      </a-form-item>

      <a-form-item
        label="联系方式"
        name="contact"
        :rules="[{ required: true, message: '请输入联系方式' }]"
      >
        <a-input
          v-model:value="formState.contact"
          placeholder="请输入手机号/微信号"
        />
      </a-form-item>

      <p class="privacy-notice">
        提供联系方式将由我们的客服团队处理您的需求，我们确保您的隐私安全
      </p>

      <a-form-item>
        <a-button type="primary" html-type="submit" block>提交需求</a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { message } from 'ant-design-vue'

const showOther = ref(false)
const formState = reactive({
  demandType: undefined,
  otherType: '',
  expectedDate: null,
  description: '',
  contact: ''
})

const handleTypeChange = (value) => {
  showOther.value = value === 'other'
}

const onFinish = (values) => {
  console.log('提交的数据：', values)
  message.success('需求提交成功！')
  // 重置表单
  Object.assign(formState, {
    demandType: undefined,
    otherType: '',
    expectedDate: null,
    description: '',
    contact: ''
  })
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 40px;
}

h1 {
  font-size: 24px;
  color: #333;
  margin-bottom: 8px;
}

.subtitle {
  font-size: 16px;
  color: #666;
}

.privacy-notice {
  font-size: 14px;
  color: #666;
  margin: 16px 0;
  text-align: center;
}
</style> 