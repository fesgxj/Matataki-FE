<template>
  <div class="notice-creator">
    <span class="warn-tip">{{ $t('the-coin-has-insufficient-liquidity-and-cannot-be-unlocked-temporarily') }}</span>
    <el-button
      type="primary"
      plain
      size="mini"
      :disabled="noticeDisabled"
      :loading="loading"
      @click="notice"
    >
      {{ $t('notify-the-author') }}
    </el-button>
  </div>
</template>
<script>
export default {
  name: 'NoticeCreator',
  props: {
    postId: {
      type: [ Number, String ],
      required: true
    },
    tokenId: {
      type: [ Number, String ],
      required: true
    },
  },
  data() {
    return {
      noticeDisabled: false,
      loading: false
    }
  },
  methods: {
    async notice() {
      if (this.tokenId && this.postId) {
        this.loading = true
        await this.$API.insufficientLiquidity({ postId: this.postId, tokenId: this.tokenId })
        this.noticeDisabled = true
        this.loading = false
        this.$message({
          showClose: true,
          message: '通知成功~',
          type: 'success'
        })
      } else {
        this.$message({
          showClose: true,
          message: '数据出错，刷新后重试',
          type: 'error'
        })
      }
    }
  }
}
</script>
<style lang="less">
.notice-creator {
  margin-top: 10px;
  .warn-tip {
    color: #FB6877!important;
    font-size: 12px;
  }
}
</style>
