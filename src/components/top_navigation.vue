<template>
  <div class="bg-gray-800 text-white p-4">
    <div class="container mx-auto flex items-center justify-between">
      <div class="flex items-center">
        <img src="../../public/Vector.svg" alt="Logo" class="h-5 w-auto mr-2" />
        <hr />
        <div class="text-lg font-bold mx-2">ハイライト</div>
      </div>
      <div class="flex justify-end">
        <!-- <el-button type="primary"  >Introduction</el-button> -->
        <el-button type="primary" @click="centerDialogVisible = true" class="mx-3"
          >Introduction</el-button
        >

        <el-dialog v-model="centerDialogVisible" class="w-1/2" align-center>
          <template #title>
            <div class="flex items-center justify-center">
              <img src="../../public/Vector.svg" alt="Logo" class="h-10" />
              <!-- Logo -->
              <span class="mx-5 text-sky-400 text-2xl">Welcome to ハイライト</span>
              <!-- Title Text -->
            </div>
          </template>
          <p class="text-lg text-gray-600">
            Welcome to ハイライト, your go-to platform for enhancing coding efficiency through
            advanced code highlighting. Tailored for developers and coding enthusiasts alike, our
            tool supports a wide range of programming languages, offering a seamless coding
            experience with real-time syntax highlighting.
          </p>
          <p class="text-lg text-gray-600">
            <strong>How to Use:</strong><br />
            1. Start typing or paste your code in the left pane.<br />
            2. The system will highlight the display based on the selected language.<br />
            3. If no language is selected, it will automatically scan and highlight<br />
            3. Adjust the pane sizes as needed for a comfortable coding and review experience.
          </p>
          <template #footer>
            <div class="dialog-footer">
              <el-button @click="centerDialogVisible = false">Close</el-button>
            </div>
          </template>
        </el-dialog>
        <el-button type="primary">Issue</el-button>
        <el-divider direction="vertical" class="h-8 mx-3" />
        <el-switch
          v-model="dark"
          :active-action-icon="Moon"
          :inactive-action-icon="Sunny"
          @change="changeTheme"
        ></el-switch>
        <el-divider direction="vertical" class="h-8 mx-3" />
        <img
          class="img mx-1 transition-transform transform hover:scale-110 active:scale-90"
          src="../image/Mail.svg"
          alt=""
          @click="sendEmail"
        />
        <img
          class="img mx-1 transition-transform transform hover:scale-110 active:scale-90"
          src="../image/Github.svg"
          alt=""
          @click="redirectToGithub"
        />
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
import $bus from '../bus'
import { Moon, Sunny } from '@element-plus/icons-vue'
const dark = ref<boolean>(false)
const centerDialogVisible = ref(false)
const changeTheme = () => {
  const root = document.documentElement
  dark.value ? (root.className = 'dark') : (root.className = '')
  $bus.emit('changeTheme', dark.value)
}

const sendEmail = () => {
  const recipientEmail: string = 'zhangtao4901@gmail.com'
  const subject: string = 'About the highlight'
  const body: string = ''
  const mailtoLink: any = `mailto:${recipientEmail}?subject=${subject}&body=${body}`
  window.open(mailtoLink)
}
const redirectToGithub = () => {
  window.open('https://github.com/Cream26', '_blank')
}
</script>
