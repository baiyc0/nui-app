<template>
  <view class="content">
    <view>
      <view class="itemTitle" v-html="number + '、' + stem"></view>
      <view v-for="(i, index) in response_points" :key="index">
        <view v-if="i.radio.val == answer && selectAnswer != ''" class="itemSelectText" v-html="i.radio.val + '、' + i.radio.text"></view>
        <view v-else-if="i.radio.val == selectAnswer" class="itemSelectsText2" v-html="i.radio.val + '、' + i.radio.text"></view>
        <view v-else class="itemText" @click="onSelectAnswer(i.radio.val)" v-html="i.radio.val + '、' + i.radio.text"></view>
      </view>
    </view>
    <view class="row-parent row-item">
      <button class="button" @click="onGoBack" style="display: inline; margin-right: 50rpx; margin-left: 100rpx">上一题</button>
      <button class="button" @click="onShowAnalysis" style="display: inline; margin-right: 50rpx">题解</button>
      <button class="button" @click="nextPage" style="display: inline">下一题</button>
    </view>
    <view class="itemText" v-if="isShowAnalysis">
      {{ '正确答案：' + answer }}
      <text class="itemText">题解：</text>
      <view class="itemText" v-html="analysis"></view>
    </view>
  </view>
</template>

<script>
import index from './index.vue';

export default {
  data() {
    var dataList = require('@/static/json/anwser.json').items;
    var item = dataList[0];
    var question = item.questions[0];
    return {
      index: 0,
      number: 1,
      stem: question.stem,
      response_points: question.response_points,
      answer: question.answer,
      analysis: question.analysis,
      isShowAnalysis: false,
      selectAnswer: '',
    };
  },
  mounted() {},
  onLoad: function (option) {
    this.getData();
  },
  methods: {
    getData() {
      var indexC = this.index * 1;
      var dataList = require('@/static/json/anwser.json').items;
      var item = dataList[indexC];
      console.log('1111', item);
      var question = item.questions[0];

      this.number = indexC + 1;
      this.stem = question.stem;
      this.response_points = question.response_points;
      this.answer = question.answer;
      this.analysis = question.analysis;

      // if (indexC == null || this.dataList.lenght <= indexC) {
      //   indexC = 0;
      // }
      this.index = indexC;
    },
    onGoBack() {
      console.log(this);
      this.selectAnswer = '';
      this.isShowAnalysis = false;

      this.index = this.index - 0 - 1;
      this.getData();
    },
    onShowAnalysis() {
      this.isShowAnalysis = true;
    },
    nextPage() {
      console.log(this.index);
      //   uni.navigateTo({
      //     url: 'answer?index=' + (),
      //   });
      this.isShowAnalysis = false;
      this.selectAnswer = '';
      this.index = this.index - 0 + 1;
      this.getData();
    },
    onSelectAnswer(selectAnswer) {
      if (this.selectAnswer == '') {
        this.selectAnswer = selectAnswer;
        this.isShowAnalysis = true;
      }
    },
  },
};
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: start;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin: 200rpx auto 50rpx auto;
}
.text-area {
  display: flex;
  justify-content: start;
}
.itemTitle {
  display: block;
  margin: 32rpx;
  font-size: 36rpx;
  color: #8f8f94;
}
.itemText {
  display: block;
  align-content: start;
  margin: 32rpx;
  font-size: 20rpx;
  color: #121213;
}
.itemSelectText {
  background: #71f802;
  display: block;
  align-content: start;
  margin: 32rpx;
  font-size: 20rpx;
  color: #121213;
}
.itemSelectsText2 {
  background: #f70509;
  display: block;
  align-content: start;
  margin: 32rpx;
  font-size: 20rpx;
  color: #121213;
}
</style>
