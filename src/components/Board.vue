<template>
  <div class="board">
    <Btn v-for="n in 17" :key="n" :num="n" @accepted="onClickChild" />
  </div>
</template>

<script>
import Btn from "../components/Btn";

export default {
  name: "Board",
  components: {
    Btn,
  },
  props: {
    msg: String,
    s: String,
  },

  data: function() {
    return {
      counter: "1",
      test: "here is the test",
      btnArr: Array.from(Array(17).keys()),
    };
  },
  mounted() {},
  created() {},

  methods: {
    onClickChild(value) {
      console.log("the app.vue", value); // someValue
    },
  },
};
</script>

<style>
.board {
  display: grid;
  width: 30%;
  grid-template-columns: repeat(3, 1fr);
  background-color: red;
}
</style>
