<template>
  <div class="bg-gray-800 text-white p-4">
    <div class="container mx-auto flex items-center justify-between">
      <div class="flex items-center">
        <img src="../../public/Vector.svg" alt="Logo" class="h-5 w-auto mr-2" />
        <hr />
        <div class="text-lg font-bold mx-2">ハイライト</div>
      </div>
      <div class="flex justify-end">
        <el-button type="info">Success</el-button>
        <el-button type="info">Success</el-button>
        <el-button type="info">Success</el-button>
        <el-divider direction="vertical" class="h-8"/>
        <el-switch
          v-model="dark"
          :active-action-icon="Moon"
          :inactive-action-icon="Sunny"
          @change="changeTheme"
        ></el-switch>
        <el-divider direction="vertical" class="h-8"/>
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
import { Moon, Sunny } from '@element-plus/icons-vue'
const dark = ref<boolean>(false)
const changeTheme = () => {
  const root = document.documentElement
  dark.value ? (root.className = 'dark') : (root.className = '')
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
