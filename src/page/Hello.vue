<template lang="pug">
  .hello
    div
    svg(width="100%" height="600px" w)
      circle(v-for="c in circle" v-bind="c")

</template>

<script>

import Vue from 'vue';
import * as _ from 'lodash';
import MixinBase from '../components/mixin-base';
import { store } from '../vuex/store';
import card from '../components/card';
import * as Util from '../util';

console.log(Util);

// mixin Vue 생명주기와 관련하여 TODO 가 있는 경우 사용한다.
// library , util 기능이 필요한경우에는 mixin 이 아닌 prototype 을 사용한다.
Vue.component('card', card);

export default {
  store,
  mixins: [MixinBase],
  mounted() {
    for (let i = 0; i < 20; i += 1) {
      this.circle.push({
        cx: 80 * i,
        cy: 0,
        r: 50,
        type: 'red',
        data: 'w'
      });
    }
    setInterval(() => {
      for (let i = 0; i < 20; i += 1) {
        setTimeout(() => {
          this.circle[i].cy = 100;
          this.circle[i].fill = '#cb3745';
        }, 50 * i);
      }
    }, 2000);

    setTimeout(() => {
      setInterval(() => {
        for (let i = 0; i < 20; i += 1) {
          setTimeout(() => {
            this.circle[i].cy = 300;
            this.circle[i].fill = '#e99a2b';
          }, 50 * i);
        }
      }, 2000);
    }, 1000);
  },
  data() {
    return {
      multiply: 1,
      circle: [{
        cx: 100,
        cy: 100,
        r: 50,
        type: 'red',
        data: 'w'
      }, {
        cx: 300,
        cy: 100,
        r: 50,
        type: 'red',
        data: 't'
      }, {
        cx: 500,
        cy: 100,
        r: 50,
        type: 'red',
        data: 'f'
      }],
      testNumber: '10000000',
      msg: 'Welcome to Hanu Vue Template',
      cards: [],
      name: '',
      age: '',
      gender: '',
      testObject: {}
    };
  },
  computed: {
    getDisplayText() {
      return `${this.name}은 나이가 ${this.age}인 ${this.gender}입니다`;
    },
    count() {
      return this.$store.state.count;
    },
    getTestObject() {
      return this.testObject;
    },
    getPosition() {
      return {
        left: `${this.posX}px`,
        top: `${this.posY}px`
      };
    }
  },
  methods: {
    removeText(i, k) {
      delete this.testObject[i][k];
      // Vue.delete(this.testObject[i], k);
      console.log(this.testObject);
    },
    increment() {
      this.$store.commit('increment', { inc: 1 });
    },
    decrement() {
      this.$store.commit('increment', { inc: -1 });
    },
    async mousemoved() {
      console.log(this);
    }
  },
  // eslint-disable-next-line object-shorthand
  created: function () {
    // todo get data from server
    console.log(this);
    this.baseMethod();
    setTimeout(() => {
      for (let i = 0; i < 5; i += 1) {
        this.cards.push({ name: `name${i}` });
      }
    }, 1000);
    for (let i = 0; i < 2; i += 1) {
      this.testObject[`${i}`] = { a: 10, b: 20, c: 30 };
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
svg
  circle
    transition: all .3s
  &[w]
    circle[data=t]
      r: 30px !important

li
  background: #333
  color: #fff
  text-decoration: none

.card-group
  display: flex

</style>
