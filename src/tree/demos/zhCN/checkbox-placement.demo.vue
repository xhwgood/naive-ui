<markdown>
# 复选框位置
</markdown>

<script lang="ts">
import type { TreeOption } from 'naive-ui'
import { repeat } from 'seemly'
import { defineComponent, ref } from 'vue'

function createData(level = 4, baseKey = ''): TreeOption[] | undefined {
  if (!level)
    return undefined
  return repeat(6 - level, undefined).map((_, index) => {
    const key = `${baseKey}${level}${index}`
    return {
      label: createLabel(level),
      key,
      children: createData(level - 1, key)
    }
  })
}

function createLabel(level: number): string {
  if (level === 4)
    return '道生一'
  if (level === 3)
    return '一生二'
  if (level === 2)
    return '二生三'
  if (level === 1)
    return '三生万物'
  return ''
}

export default defineComponent({
  setup() {
    return {
      data: createData(),
      defaultExpandedKeys: ref(['40', '4030', '403020']),
      defaultCheckedKeys: ref(['40302010']),
      updateCheckedKeys: (v: string[]) => {
        console.log('updateCheckedKeys', v)
      }
    }
  }
})
</script>

<template>
  <n-tree
    checkable
    block-node
    checkbox-placement="right"
    :data="data"
    :default-expanded-keys="defaultExpandedKeys"
    :default-checked-keys="defaultCheckedKeys"
    @update:checked-keys="updateCheckedKeys"
  />
</template>
