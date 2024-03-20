<template>
  <view class="content">
    <view>
      页码 {{ nums }}
      <text v-for="(item, index) in nums" :key="index">
        <text @click="selectNum(item)">{{ item }}</text>
      </text>
    </view>
  </view>
</template>

<script>
export default {
  name: 'SelectIndex',
  props: ['nums'], // props 组件的属性，由父级传递
  data() {
    return {
      index: 0,
    };
  },

  methods: {
    selectNum(num) {
      console.log(num);
      this.$emit('getNum', num); //  $emit 组件的注册的事件，可以给响应给父级，并传参数
    },
  },
};
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: start;
}
</style>
