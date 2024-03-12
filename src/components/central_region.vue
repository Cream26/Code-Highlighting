<template>
  <div class="flex flex-grow overflow-hidden bg-slate-700" ref="container">
    <!-- Left Pane: Text Editor -->
    <div
      class="flex-none bg-white shadow rounded p-4"
      :style="{ width: leftWidth + 'px' }"
    >
      <textarea
        class="w-full h-64 border p-2"
        placeholder="Write something..."
      ></textarea>
    </div>

    <!-- Draggable Divider -->
    <div
      class="cursor-col-resize bg-gray-400 mx-2 w-2"
      @mousedown="startDrag"
    ></div>

    <!-- Right Pane: Code Preview -->
    <div class="flex-grow bg-white shadow rounded p-4 overflow-auto">
      <h2 class="text-lg font-semibold mb-2">Code Preview</h2>
      <!-- Your code preview container -->
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const container = ref<HTMLElement | null>(null);
const leftWidth = ref(300); // Initial width of the left pane
let startX = 0; // Initial X position when dragging starts
let startWidth = 0; // Initial width of the left pane when dragging starts

const MIN_LEFT_WIDTH = 400; // Minimum width of the left pane
const MIN_RIGHT_WIDTH = 400; // Minimum width of the right pane

const startDrag = (event: MouseEvent) => {
  // Prevent text selection while dragging
  event.preventDefault();

  startX = event.clientX;
  startWidth = leftWidth.value;
  document.addEventListener('mousemove', doDrag);
  document.addEventListener('mouseup', stopDrag);
};

const doDrag = (event: MouseEvent) => {
  if (!container.value) return;

  const currentX = event.clientX;
  const deltaX = currentX - startX;
  const newWidth = startWidth + deltaX;

  const containerWidth = container.value.offsetWidth;
  if (newWidth > MIN_LEFT_WIDTH && (containerWidth - newWidth) > MIN_RIGHT_WIDTH) {
    leftWidth.value = newWidth;
  }
};

const stopDrag = () => {
  document.removeEventListener('mousemove', doDrag);
  document.removeEventListener('mouseup', stopDrag);
};

onMounted(() => {
  if (container.value) {
    const containerRect = container.value.getBoundingClientRect();
    leftWidth.value = containerRect.width / 2; // Initially set to half of container width
  }
});
</script>
