<template>
  <div class="board">
    <Btn
      class="btn"
      v-for="n in calculations"
      :key="n"
      :num="n"
      @accepted="onClickChild"
    />
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
    calculations: Array,
  },
  // emits: ["displayNumber"],
  data: function() {
    return {
      counter: "1",
      test: "here is the test",
      btnArr: Array.from(Array(17).keys()),
    };
  },
  methods: {
    onClickChild(value) {
      console.log("the app.vue", value); // someValue
      this.$emit("displayNumber", value);
    },
  },
  mounted() {},
  created() {},
};
</script>

<style>
.board {
  display: grid;
  width: 25%;
  grid-template-columns: repeat(4, 1fr);
}
</style>
