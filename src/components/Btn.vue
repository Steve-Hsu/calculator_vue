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
  emits: ["accepted"],
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
    console.log("the num in btn.vue", this.num);
    switch (this.num) {
      case 10:
        this.label = 0;
        break;
      case 11:
        this.label = "+";
        break;
      case 12:
        this.label = "-";
        break;
      case 13:
        this.label = "/";
        break;
      case 14:
        this.label = "x";
        break;
      case 15:
        this.label = "=";
        break;
      case 16:
        this.label = "c";
        break;
      case 17:
        this.label = ".";
        break;
      default:
        this.label = `${this.num}`;
        break;
    }

    // console.log("test", this.label);
  },
};
</script>

<style scoped>
.btn {
  width: 5rem;
  height: 5rem;
  margin: 5px;
}
</style>
