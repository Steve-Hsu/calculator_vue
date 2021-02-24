<template>
  <div>{{ displayNumber }}</div>
  <Board
    msg="Welcome to Your Vue.js App"
    s="Steve"
    @displayNumber="onClickChild"
  />
</template>

<script>
import Board from "./components/Board.vue";

export default {
  name: "App",
  components: {
    Board,
  },
  data: function() {
    return {
      displayNumber: "0",
      enteredKey: "",
      cal: "",
      oldNum: "",
      newNum: "",
      oldDecimalIdx: 0,
      newDecimalIdx: 0,
      oldDecimalLength: 0,
      newDecimalLength: 0,
      oldConvertKey: 1,
      newConvertKey: 1,
      convertRoot: 0,
      oldConvertedNum: 0,
      newConvertedNum: 0,
    };
  },
  methods: {
    onClickChild(value) {
      console.log("the app.vue", value); // someValue
      this.$emit("displayNumber", value);
      this.enteredKey = value;

      switch (this.enteredKey) {
        case "+":
        case "-":
        case "x":
        case "/":
          this.oldNum = this.displayNumber;
          this.displayNumber = "0";
          this.cal = this.enteredKey;
          break;
        case "=":
          if (this.oldNum.indexOf(".") > -1 || this.newNum.indexOf(".") > -1) {
            this.oldDecimalIdx = this.oldNum.indexOf(".");
            this.newDecimalIdx = this.newNum.indexOf(".");
            this.oldDecimalLength =
              this.oldNum.length - this.oldNum.indexOf(".");
            this.newDecimalLength =
              this.newNum.length - this.newNum.indexOf(".");
            this.oldConvertKey = Math.pow(10, this.oldDecimalLength - 1);
            this.newConvertKey = Math.pow(10, this.newDecimalLength - 1);
            this.convertRoot =
              this.oldConvertKey > this.newConvertKey
                ? this.oldConvertKey
                : this.newConvertKey;
            switch (this.cal) {
              case "+":
                this.oldConvertedNum = Math.round(
                  Number(this.oldNum) * this.convertRoot
                );
                this.newConvertedNum = Math.round(
                  Number(this.newNum) * this.convertRoot
                );

                this.oldNum = String(
                  (Number(this.oldConvertedNum) +
                    Number(this.newConvertedNum)) /
                    this.convertRoot
                );

                break;
              case "-":
                this.oldConvertedNum = Math.round(
                  Number(this.oldNum) * this.convertRoot
                );
                this.newConvertedNum = Math.round(
                  Number(this.newNum) * this.convertRoot
                );

                this.oldNum = String(
                  (Number(this.oldConvertedNum) -
                    Number(this.newConvertedNum)) /
                    this.convertRoot
                );

                break;
              case "x":
                this.oldConvertedNum = Math.round(
                  Number(this.oldNum) * this.oldConvertKey
                );
                this.newConvertedNum = Math.round(
                  Number(this.newNum) * this.newConvertKey
                );

                this.oldNum = String(
                  (Number(this.oldConvertedNum) *
                    Number(this.newConvertedNum)) /
                    (this.oldConvertKey * this.newConvertKey)
                );
                break;
              case "/":
                this.oldConvertedNum = Math.round(
                  Number(this.oldNum) * this.convertRoot
                );
                this.newConvertedNum = Math.round(
                  Number(this.newNum) * this.convertRoot
                );
                this.oldNum = String(
                  Number(this.oldConvertedNum) / Number(this.newConvertedNum)
                );
                break;
              default:
            }
            // this.displayNumber = this.oldNum;
          } else {
            switch (this.cal) {
              case "+":
                this.oldNum = String(Number(this.oldNum) + Number(this.newNum));
                break;
              case "-":
                this.oldNum = String(Number(this.oldNum) - Number(this.newNum));
                break;
              case "x":
                this.oldNum = String(Number(this.oldNum) * Number(this.newNum));
                break;
              case "/":
                this.oldNum = String(Number(this.oldNum) * Number(this.newNum));
                break;
              default:
            }
            // this.displayNumber = this.oldNum;
          }
          console.log("the oldnumber", this.oldNum);
          this.displayNumber = this.oldNum || this.displayNumber;
          break;
        case "c":
          this.oldNum = "0";
          this.cal = "";
          this.displayNumber = "0";
          break;
        case ".":
          if (this.displayNumber.indexOf(".") === -1) {
            this.displayNumber = this.displayNumber + ".";
          }
          break;
        case 0:
          if (this.displayNumber !== "0") {
            this.displayNumber = this.displayNumber + "0";
          }
          break;
        default:
          if (this.displayNumber !== "0") {
            this.displayNumber = this.displayNumber + value;
          } else {
            this.displayNumber = value;
          }
          this.newNum = this.displayNumber;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: grid;
  place-items: center;
}
</style>
