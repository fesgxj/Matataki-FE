<template>
  <el-dropdown class="language-toggle">
    <span class="el-dropdown-link">
      {{ currentLanguage }}<i class="el-icon-arrow-down el-icon--right" />
    </span>
    <el-dropdown-menu slot="dropdown">
      <el-dropdown-item>
        <span @click="changeLanguage('zh')">
          简体中文
        </span>
      </el-dropdown-item>
      <el-dropdown-item>
        <span @click="changeLanguage('en')">
          English
        </span>
      </el-dropdown-item>
      <el-dropdown-item>
        <span @click="changeLanguage('ja')">
          Japanese
        </span>
      </el-dropdown-item>
    </el-dropdown-menu>
  </el-dropdown>
</template>

<script>

export default {
  data() {
    return {

    }
  },
  computed: {
    // 当前语言
    currentLanguage() {
      const language = {
        zh: '简体中文',
        en: 'English',
        ja: 'Japanese',
      }
      return language[this.$i18n.locale] || '默认'
    }
  },
  methods: {
    changeLanguage(lang) {
      this.$i18n.setLocaleCookie(lang)
      this.$router.go(0)
    }
  }
}
</script>

<style lang="less" scoped>
.language-toggle {
  span {
    display: block;
  }
}
</style>
