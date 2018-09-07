<template lang="pug">
  .hello
    h3 WT?
    .card-group
      template(v-for="card in cards")
        card(:cardName="card.name")

</template>

<script>

import Vue from 'vue';
import { store } from '../vuex/store';
import card from '../components/card';

Vue.component('card', card);

export default {
  name: 'HelloWorld',
  store,
  data() {
    return {
      msg: 'Welcome to Hanu Vue Template',
      cards: []
    };
  },
  computed: {
    count() {
      return this.$store.state.count;
    },
    getPosition() {
      return {
        left: `${this.posX}px`,
        top: `${this.posY}px`
      };
    }
  },
  methods: {
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

    setTimeout(() => {
      for (let i = 0; i < 5; i += 1) {
        this.cards.push({ name: `name${i}` });
      }
    }, 1000);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
li
  background : #333
  color : #fff
  text-decoration: none
.card-group
  display: flex

</style>
