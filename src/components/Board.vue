<template>
     <div class="board">
           <div v-for="n in 17" :key="n">
               <Btn :num="n" />

  </div>
    </div>
</template>

<script>
import Btn from '../components/Btn'

export default {
    name:"Board",
    components: {
    Btn
    },
    props:{
        msg:String,
        s:String,
    },
    data: function () {
        return {
            counter: "1",
            test : "here is the test",
            btnArr: Array.from(Array(17).keys()),
        }
    },
    mounted () {

    },
    created () {
        
    //    this.btnArr = this.btnArr.map((i)=>{
    //         return `name of ${i}`
    //         });
    //         console.log("the created",this.btnArr);
    }
}
</script>

<style>
.board{
 display: grid;
  width: 30%;
  grid-template-columns: repeat(3, 1fr);
  background-color: red;
}

</style>