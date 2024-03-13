<template>
  <div class="flex flex-col flex-grow overflow-hidden bg-slate-700" ref="container">
    <!-- Toolbar & Main Work Area -->
    <div class="flex flex-grow overflow-hidden">
      <!-- Left Pane: Text Editor + Toolbar -->
      <div
        class="flex flex-col bg-slate-700 shadow rounded flex-none"
        :style="{ width: leftWidth + 'px' }"
      >
        <!-- Left Toolbar Area -->
        <div class="bg-slate-700 p-2 flex justify-end">
          <el-select v-model="value" placeholder="language" style="width: 110px">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
        </div>
        <hr />
        <!-- Text Editor -->
        <div class="h-full" ref="editorContainer"></div>
      </div>

      <!-- Draggable Divider -->
      <div
        class="cursor-col-resize bg-gray-400 mx-1 w-2 flex-none"
        :style="{ left: dividerLeft + 'px' }"
        @mousedown="startDrag"
      ></div>

      <!-- Right Pane: Code Preview + Toolbar -->
      <div
        class="flex flex-col bg-slate-700 shadow rounded overflow-hidden flex-grow"
        :style="{ width: rightWidth + 'px' }"
      >
        <!-- Right Toolbar Area -->
        <div class="flex bg-slate-700 p-2 shadow">
          <el-button type="primary" @click="highlightCode">Highlighting</el-button>
        </div>
        <hr />
        <!-- Code Preview -->
        <div class="h-full" ref="previewContainer"></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import * as monaco from 'monaco-editor'

const editorContainer = ref(null)
const previewContainer = ref(null)
let leftEditor
let previewEditor
const container = ref<HTMLElement | null>(null)
const leftWidth = ref(0) // Initial width of the left pane
const rightWidth = ref(0) // Initial width of the right pane
let startX = 0 // Initial X position when dragging starts
let startLeftWidth = 0 // Initial width of the left pane when dragging starts
let startRightWidth = 0 // Initial width of the right pane when dragging starts

const MIN_PANE_WIDTH = 400 // Minimum width of the panes

const startDrag = (event: MouseEvent) => {
  // Prevent text selection while dragging
  event.preventDefault()

  startX = event.clientX
  startLeftWidth = leftWidth.value
  startRightWidth = rightWidth.value
  document.addEventListener('mousemove', doDrag)
  document.addEventListener('mouseup', stopDrag)
}

const doDrag = (event: MouseEvent) => {
  if (!container.value) return

  const currentX = event.clientX
  const deltaX = currentX - startX
  const newLeftWidth = startLeftWidth + deltaX
  const newRightWidth = startRightWidth - deltaX

  if (newLeftWidth > MIN_PANE_WIDTH && newRightWidth > MIN_PANE_WIDTH) {
    leftWidth.value = newLeftWidth
    rightWidth.value = newRightWidth
  }
}

const stopDrag = () => {
  document.removeEventListener('mousemove', doDrag)
  document.removeEventListener('mouseup', stopDrag)
}
const highlightCode = () => {
   console.log("Current language selection: ", value.value);
  if (!leftEditor || !previewEditor || !value.value) return;

  // 获取左侧编辑器的内容
  const code = leftEditor.getValue();

  // 更新右侧预览编辑器的内容
  previewEditor.setValue(code);

  // 重点在这里：设置右侧编辑器的语言，触发语法高亮
  monaco.editor.setModelLanguage(previewEditor.getModel(), value.value);
};


onMounted(() => {
  // Set initial width for left and right panes
  const containerWidth = container.value?.offsetWidth || 0
  leftWidth.value = containerWidth / 2
  rightWidth.value = containerWidth / 2

  if (editorContainer.value) {
    leftEditor = monaco.editor.create(editorContainer.value, {
      value: [
        '# Markdown Editor',
        '',
        'Start typing Markdown here and see the preview on the right.'
      ].join('\n'),
      language: 'plaintext',
      theme: 'vs-light',
      automaticLayout: true,
      contextmenu: false,
      scrollbar: {
        verticalScrollbarSize: 6,
        horizontalScrollbarSize: 6
      },
      fontSize: 15,
      tabSize: 2,
      scrollBeyondLastLine: false
    })
    
  }
  if (previewContainer.value) {
    previewEditor = monaco.editor.create(previewContainer.value, {
      value: '',
      language: 'plaintext',
      theme: 'vs-light',
      readOnly: true,
      automaticLayout: true,
      scrollbar: {
        verticalScrollbarSize: 6,
        horizontalScrollbarSize: 6
      },
      fontSize: 15,
      scrollBeyondLastLine: false
    })
  }
})

const dividerLeft = ref(0)
const value = ref('')
const options = [
  { value: 'javascript', label: 'JavaScript' },
  { value: 'markdown', label: 'Markdown' },
  { value: 'java', label: 'Java' },
  { value: 'python', label: 'Python' },
  { value: 'csharp', label: 'C#' },
  { value: 'cpp', label: 'C++' },
  { value: 'ruby', label: 'Ruby' },
  { value: 'php', label: 'PHP' },
  { value: 'swift', label: 'Swift' },
  { value: 'kotlin', label: 'Kotlin' },
  { value: 'typescript', label: 'TypeScript' },
  { value: 'go', label: 'Go' },
  { value: 'rust', label: 'Rust' },
  { value: 'sql', label: 'SQL' },
  { value: 'html', label: 'HTML' },
  { value: 'css', label: 'CSS' }
]
</script>