<template>
  <div class="Help">
    <BaseHeader>
      <template v-slot:center>
        <span class="f16 fb">帮助与设置</span>
      </template>
      <template v-slot:right>
        <span class="f14">我的反馈</span>
      </template>
    </BaseHeader>
    <div class="content">
      <!-- 帮助页面内容占位 -->
      <div class="help-placeholder">
        <p>帮助与反馈功能开发中...</p>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
defineOptions({
  name: 'Help'
})
</script>

<style scoped lang="less">
@import '../../assets/less/index';

.Help {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  overflow: auto;
  color: white;
  font-size: 14rem;

  .content {
    margin-top: 60rem;
    height: calc(var(--vh, 1vh) * 100 - 60rem);

    .help-placeholder {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      color: #999;
    }
  }
}
</style>
