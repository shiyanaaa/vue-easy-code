<script setup lang="ts">
import { computed, ref } from 'vue'
import { type Attrs } from '@/type/type'
import Tree from './tree.vue'
const props = defineProps({
  attr: {
    type: Object as () => Attrs,
    default: () => ({})
  },
  index: {
    type: Number,
    default: 0
  }
})
const style = computed(() => {
  return {
    textIndent: `${(props.index + 1) * 2}em`
  }
})
const innerStyle = computed(() => {
  return {
    textIndent: `${(props.index + 2) * 2}em`
  }
})
const replaceOnEventWithVOn = (code: string) => {
  // 使用正则表达式匹配 on[大写字母][小写字母...]
  const regex = /on([A-Z][a-z]+)/g

  // 替换 on[事件名] 为 @[小写首字母事件名]
  return code.replace(
    /on([A-Z][a-z]+)/g,
    (match, p1: any) => `@${p1.charAt(0).toLowerCase()}${p1.slice(1)}`
  )
}
function toLine(name: string) {
  return name.replace(/([A-Z])/g, '_$1').toLowerCase()
}
const showAttr = computed(() => {
  return Object.keys(props.attr.attrs)
    .map((key) => {
      if (/^on[A-Z]/.test(key)) {
        return `<span class="code-attr">${replaceOnEventWithVOn(key)}</span>="<span class="code-fun">aaa</span>"`
      } else if (key === 'style') {
        return `<span class="code-attr">style</span>="${Object.keys(props.attr.attrs.style)
          .map(
            (key) =>
              `<span class="code-style">${toLine(key)}</span>:<span class="code-style-value">${props.attr.attrs.style[key]}</span>`
          )
          .join('; ')}"`
      }
      return `<span class="code-attr">${key}</span>="<span class="code-attr-value">${props.attr.attrs[key]}</span>"`
    })
    .join(' ')
})
</script>
<script lang="ts"></script>
<template>
  <div class="code-line" :style="style">
    <span class="code-tag-out">&lt;</span><span class="code-tag">{{ props.attr.component }}</span>
    <span v-html="showAttr"></span><span class="code-tag-out">&gt;</span>
  </div>
  <div class="code-line" v-if="props.attr.inner" :style="innerStyle">{{ props.attr.inner }}</div>
  <Tree v-if="props.attr.children" :attrs="props.attr.children" :index="props.index + 1"></Tree>
  <div class="code-line" :style="style">
    <span class="code-tag-out">&lt;/</span><span class="code-tag">{{ props.attr.component }}</span
    ><span class="code-tag-out">&gt;</span>
  </div>
</template>

<style lang="scss" scoped></style>
