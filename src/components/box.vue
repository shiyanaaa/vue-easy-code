<script setup lang="ts">
import { ref } from 'vue'
import { type Attrs } from '@/type/type'

const props = defineProps({
  attrs: {
    type: Array as () => Attrs[],
    default: () => []
  }
})
</script>
<script lang="ts">
export default {
  name: 'box' //给组件命名
}
</script>
<template>
  <template v-for="item in props.attrs" :key="item.id">
    <component :is="item.component" v-bind="item.attrs">
      <template v-if="item.inner">{{ item.inner }}</template>
      <box v-if="item.children" :attrs="item.children"></box>
    </component>
  </template>
</template>

<style lang="scss" scoped></style>
