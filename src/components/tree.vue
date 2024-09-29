<script setup lang="ts">
import { computed, ref } from 'vue'
import { type Attrs } from '@/type/type'
import treeItem from './treeItem.vue'
const props = defineProps({
  attrs: {
    type: Array as () => Attrs[],
    default: () => []
  },
  index: {
    type: Number,
    default: 0
  }
})
</script>

<template>
  <div class="code-line" v-if="props.index === 0">
    <span class="code-tag-out">&lt;</span><span class="code-tag">template</span
    ><span class="code-tag-out">&gt;</span>
  </div>
  <treeItem v-for="item in props.attrs" :key="item.id" :attr="item" :index="props.index"></treeItem>
  <div class="code-line" v-if="props.index === 0">
    <span class="code-tag-out">&lt;/</span><span class="code-tag">template</span
    ><span class="code-tag-out">&gt;</span>
  </div>
</template>

<style lang="scss" scoped></style>
