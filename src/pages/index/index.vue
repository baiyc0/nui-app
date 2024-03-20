<template>
  <view class="content">
    <view>
      <button @click="goTwo" class="title6">{{ title }}</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      title: '整体管理',
    };
  },
  onLoad() {},
  methods: {
    goTwo: () => {
      uni.navigateTo({
        url: 'exercises',
      });
    },
  },
};
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin: 200rpx auto 50rpx auto;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title6 {
  margin-top: 60rpx;
  font-size: 30rpx;
  color: #8f8f94;
  display: block;
}
</style>
