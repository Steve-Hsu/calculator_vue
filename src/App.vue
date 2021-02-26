<template>
  <div class="displayNum">{{ this.thousands(displayNumber) }}</div>

  <Board
    msg="Welcome to Your Vue.js App"
    s="Steve"
    @displayNumber="onClickChild"
    :calculations="calculations"
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
      calculations: [
        "c", // 1
        "+/-",
        "%",
        "/",
        "7", // 2
        "8",
        "9",
        "x",
        "4", // 3
        "5",
        "6",
        "-",
        "1", // 4
        "2",
        "3",
        "+",
        "0", // 5
        "0",
        ".",
        "=",
      ],
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
          this.oldNum = String(this.displayNumber);
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
                this.oldNum = String(Number(this.oldNum) / Number(this.newNum));
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
        case "%":
          if (this.displayNumber !== "0") {
            this.displayNumber = this.displayNumber / 100;
          }
          break;
        case "+/-":
          if (this.displayNumber.split("")[0] !== "-") {
            this.displayNumber = "-" + this.displayNumber;
          } else {
            this.displayNumber = this.displayNumber.replace("-", "");
          }
          // this.oldNum = this.displayNumber;

          break;
        default:
          if (this.displayNumber !== "0") {
            if (
              this.displayNumber.split("")[0] === "-" &&
              this.displayNumber.split("")[1] === "0"
            ) {
              this.displayNumber = "-" + value;
            } else {
              this.displayNumber = this.displayNumber + value;
            }
          } else {
            this.displayNumber = value;
          }
          this.newNum = this.displayNumber;
      }
    },
    thousands(num) {
      console.log("the displayNumber in thousands", this.displayNumber);
      console.log("the newnum", this.newNum);
      console.log("the oldNum", this.oldNum);
      let target = String(num);
      let isDecimalNum = target.indexOf(".") > -1;
      let newStr = "";
      let tailOfDecimal = "";
      let length = target.length;
      let strArr = target.split("");
      // if (isDecimalNum) {
      //   console.log("yes in deci");

      if (isDecimalNum && target.indexOf(".") + 1 <= length) {
        tailOfDecimal = String(target.slice(target.indexOf(".")));
        // length = target.slice(0, target.indexOf("."));
        strArr = target.slice(0, target.indexOf(".")).split("");
        length = strArr.length;
      }
      for (let i = 1; i <= length; i++) {
        let theString = strArr[length - i];
        let isMultipleOfThree = i % 3 === 0;
        if (isMultipleOfThree && i !== length) {
          theString = "," + theString;
        }
        newStr = String(theString) + newStr;
      }
      return newStr + tailOfDecimal;
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
  /* background-color: black; */
}
.displayNum {
  padding: 5px 1px;
  height: 100px;
  width: 350px;
  background-color: black;
  color: white;
  font-size: 50px;
  font-weight: 800;
  font-family: "Poiret One", cursive;
  /* overflow: hidden; */
}
</style>
