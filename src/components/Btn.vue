<template>
  <button class="btn" v-on:click="onClickButton">{{ label }}</button>
</template>

<script>
export default {
  name: "Btn",
  props: {
    num: Number,
    // label:String,
  },
  // emits: ["accepted"],
  data() {
    return {
      label: String,
    };
  },
  methods: {
    onClickButton() {
      console.log("hit the btn");
      this.$emit("accepted", this.label);
    },
  },
  created() {
    this.label = `${this.num}`;
    console.log("the num in btn.vue", this.num);
  },
};
</script>

<style scoped lang="scss">
// Scss
.btn {
  width: 5rem;
  height: 5rem;
  background-color: rgba(50, 50, 50, 1);
  border-radius: 50%;
  margin: auto;
  font-family: "Poiret One", cursive;
  font-size: 30px;
  font-weight: 800;
}
</style>
