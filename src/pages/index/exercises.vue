<template>
  <view class="content">
    <view>
      <view class="itemTitle" v-html="title"></view>
      <view><SelectrNum @getNum="getNum" :nums="dataList.length"></SelectrNum> </view>
      <view v-for="(item, index) in response_points" :key="index">
        <view :class="getClass(item.radio.val)" @click="onSelectAnswer(item.radio.val)" v-html="item.radio.val + '、' + item.radio.text"></view>
      </view>
    </view>
    <view class="row-parent row-item">
      <button class="button" @click="onGoBack" style="display: inline; margin-right: 50rpx; margin-left: 100rpx">上一题</button>
      <button class="button" @click="onShowAnalysis" style="display: inline; margin-right: 50rpx">题解</button>
      <button class="button" @click="nextPage" style="display: inline">下一题</button>
    </view>
    <view class="itemText" v-if="isShowAnalysis">
      {{ '正确答案' + answer }}
      <view class="itemText" v-html="analysis"></view>
    </view>
  </view>
</template>

<script>
import SelectrNum from './selectIndex.vue'; //引入组件
export default {
  components: {
    SelectrNum, // 组件注册
  },
  data() {
    var _dataList = require('@/static/json/anwser.json').items;
    var _currentItem = _dataList[0];
    var _question = _currentItem.questions[0];

    return {
      index: 0,
      dataList: _dataList,
      title: '1、' + _question.stem,
      response_points: _question.response_points,
      answer: _question.answer,
      analysis: '题解' + _question.analysis,
      selectAnswer: '',
      isShowAnalysis: false,
    };
  },
  onLoad() {},
  watch: {
    index() {
      console.log('aaa' + this.index);
      var _currentItem = this.dataList[this.index];
      var _question = _currentItem.questions[0];
      this.title = this.index + 1 + '、' + _question.stem;
      this.response_points = _question.response_points;
      this.answer = _question.answer;
      this.analysis = '题解' + _question.analysis;
      this.isShowAnalysis = false;
      this.selectAnswer = '';
    },
  },
  computed: {
    getResponsePointClassName(val) {
      var className = 'itemText';
      if (this.selectAnswer != '') {
        if (val == this.answer) {
          className = 'itemSelectText';
        } else if (val == this.selectAnswer) {
          className = 'itemSelectsText2';
        }
      }
      return className;
    },

    questionData() {
      return this.dataList[this.index];
    },
  },
  methods: {
    getNum(num) {
      this.index = num;
    },
    getClass(val) {
      var className = 'itemText';
      if (this.selectAnswer != '') {
        if (val == this.answer) {
          className = 'itemSelectText';
        } else if (val == this.selectAnswer) {
          className = 'itemSelectsText2';
        }
      }
      return className;
    },
    onGoBack() {
      this.index = this.index - 0 - 1;
    },
    onShowAnalysis() {
      this.isShowAnalysis = !this.isShowAnalysis;
    },
    nextPage() {
      this.index = this.index - 0 + 1;
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

<style scoped>
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
