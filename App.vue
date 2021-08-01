<template>
  <view class="container">
    <text class="app__title app__title--top">Количество кубиков:</text>
    <view class="app__wrapper">
      <button title="-" :on-press="decreaseCounter"></button>
      <text class="app__counter">{{numberOfDices}}</text>
      <button title="+" :on-press="increaseCounter"></button>
    </view>
    <view class="app__dices">
      <text class="app__dice" v-for="(item, index) of numberOfDices">{{dices[index]}}</text>
    </view>
    <button class="app__button" title="SHUFFLE!" :on-press="shuffle"></button>
    <view class="app__inputs">
      <text class="app__title">Поля для записи значений:</text>
      <text-input class="app__input" v-for="item of 5"></text-input>
    </view>
  </view>
</template>

<script>
export default {
  data: function () {
    return {
      numberOfDices: 4,
      dices: []
    }
  },
  methods: {
    decreaseCounter: function () {
      if (this.numberOfDices > 4) {
        this.numberOfDices--;
      }
    },
    increaseCounter: function () {
      if (this.numberOfDices < 10) {
        this.numberOfDices++;
      }
    },
    getRandomNumber: function () {
      return this.getRandomNumberInRange(1, 6);
    },
    getRandomNumberInRange: function (min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    shuffle: function () {
      for (let i = 0; i < this.numberOfDices; i++) {
        this.$set(this.dices, i, this.getRandomNumber())
      }
    }
  },
  created: function () {
    for (let i = 0; i < this.numberOfDices; i++) {
      this.dices[i] = this.getRandomNumber();
    }
  },
  watch: {
    numberOfDices: function (newValue, oldValue) {
      if (newValue > oldValue) {
        this.dices.push(this.getRandomNumber());
      } else {
        this.dices.pop();
      }
    }
  }
}
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  flex: 1;
  padding-top: 20%;
}
.app__title {
  width: 100%;
  text-align: center;
  margin-bottom: 15px;
}
.app__wrapper {
  width: 80%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.app__dices {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-between;
  width: 80%;
  position: relative;
  margin-bottom: 20%;
  background-color: #eee;
}
.app__dice {
  text-align: center;
  width: 20%;
  margin-top: 15px;
  margin-bottom: 15px;
}
.app__inputs {
  margin-top: 50px;
  width: 80%;
}
.app__input {
  width: 100%;
  border-width: 1px;
  background-color: #eee;
  border-style: solid;
  border-radius: 5px;
  margin-bottom: 15px;
}
</style>
