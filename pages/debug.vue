<template>
  <div>
    <div style="margin: 20px 0;">
      <router-link :to="{name: 'article'}">
        <el-button>
          Home
        </el-button>
      </router-link>
    </div>
    <el-button type="primary" @click="debug(true)">
      Debug
    </el-button>
    <el-button type="primary" @click="debug(false)">
      Close Debug
    </el-button>
  </div>
</template>

<script>
import { setCookie } from '@/utils/cookie'

export default {
  layout: 'empty',
  methods: {
    async debug(val) {
      try {
        this.$message(`VConsole ${val}`)
        setCookie('VConsole', val)
      } catch (e) {
        console.log(e)
      }
    }
  }
}
</script>