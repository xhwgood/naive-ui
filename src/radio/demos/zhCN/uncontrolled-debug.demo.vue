<markdown>
# Uncontrolled Debug
</markdown>

<script lang="ts">
import { useDialog } from 'naive-ui'
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    const radioVal = ref(1)
    const dialog = useDialog()

    function handleUpdateValue(val: number) {
      dialog.info({
        title: '提示',
        content: '是否改变',
        onPositiveClick: () => {
          radioVal.value = val
        },
        positiveText: '确定',
        negativeText: '取消'
      })
    }
    return {
      radioVal,
      handleUpdateValue
    }
  }
})
</script>

<template>
  <NRadioGroup :value="radioVal" @update:value="handleUpdateValue">
    <NRadio :value="1">
      change 1
    </NRadio>
    <NRadio :value="2">
      change 2
    </NRadio>
  </NRadioGroup>
</template>
