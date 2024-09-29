<script setup lang="ts">
import { computed, ref } from 'vue'
import { type Attrs } from '@/type/type'
import Box from '@/components/box.vue'
import Tree from '@/components/tree.vue'
import { ElMessage } from 'element-plus'
const treeData = ref<Attrs[]>([
  {
    id: '1',
    component: 'div',
    attrs: {
      style: { height: '300px', background: 'blue', color: '#fff', display: 'flex' }
    },
    children: [
      {
        id: '4',
        component: 'div',
        attrs: {
          style: { height: '100px', background: 'skyblue', flex: 1 }
        },
        children: [
          {
            id: '5',
            component: 'div',
            attrs: {
              style: { height: '50px', background: 'yellow', flex: 1, display: 'flex' }
            },
            children: [
              {
                id: '7',
                component: 'el-input',
                attrs: {
                  'v-model': 'modelValue',
                  style: { background: 'orange', flex: 1 }
                }
              },
              {
                id: '8',
                component: 'el-button',
                inner: '按钮',
                attrs: {
                  onClick: () => {
                    ElMessage.success('点击')
                  }
                }
              }
            ]
          },
          {
            id: '6',
            component: 'div',
            attrs: {
              style: { height: '50px', background: 'green', flex: 1 }
            }
          }
        ]
      },
      {
        id: '4',
        component: 'div',
        attrs: {
          style: { height: '100px', background: 'pink', flex: 1 }
        }
      }
    ]
  }
])
const eventList = ref([
  { id: 1, name: 'aaa' },
  { id: 2, name: 'bbb' }
])
const varList = ref([{ id: 1, name: 'modelValue', default: '', type: 'string', varType: 'ref' }])
const aaa = () => {}
</script>
<template>
  <div class="tools">
    <el-button @click="aaa">123</el-button>
  </div>
  <div class="container">
    <div class="left">
      <Box :attrs="treeData" />
    </div>
    <div class="right">
      <Tree :attrs="treeData" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  display: flex;

  .left {
    width: 50%;
    min-height: 100vh;
  }
  .right {
    width: 50%;
    background-color: #1f1f1f;
  }
}
.tools {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 15px;
  background-color: aquamarine;
  width: 100%;
}
</style>
