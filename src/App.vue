<template>
  <div class="flex flex-col h-screen">
    <!-- Top Navigation -->
    <Top_navigation />

    <!-- Main Content -->
    <main class="flex-grow overflow-y-auto bg-slate-700">
      <div class="flex flex-col md:flex-row gap-4 container mx-auto p-4">
        <!-- Text Editor -->
        <div class="md:w-1/2 bg-white p-4 shadow rounded">
          <h2 class="text-lg font-semibold mb-2">Text Editor</h2>
          <textarea
            class="w-full border p-2 min-h-[200px]"
            placeholder="Write something..."
          ></textarea>
        </div>

        <!-- Code Highlight -->
        <div class="md:w-1/2 bg-white p-4 shadow rounded">
          <h2 class="text-lg font-semibold mb-2">Code Highlight</h2>
          <pre
            class="bg-gray-900 text-white p-3 rounded"
          ><code class="language-javascript">const hello = "Hello, world!";
console.log(hello);</code></pre>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white p-5">
      <div class="container mx-auto text-center">© 2024 Cream26. All rights reserved.</div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import Top_navigation from './components/top_navigation.vue'
;('./components/top_navigation.vue')
</script>
