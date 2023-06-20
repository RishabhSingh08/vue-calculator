
<script>
import { getCurrentInstance } from 'vue';

export default {
  name: 'Calculator',
  props: {
    msg: String
  },

  data() {
    return {
      calcVal: '',
      calcBtns: ['C', '%', '=', '+', 7, 8, 9,'-', 4, 5, 6,'*', 1, 2, 3, '/', 0, '.'],
      operators: null,
      prevCalcVal: ''
    }
  }, 
  methods: {
    action(btn){

      if(!isNaN(btn) || btn === '.')
      {
        this.calcVal += btn +''
      }

      if (btn === 'C') {
        this.calcVal = ''
      }

      if (btn === '%') {
        this.calcVal = this.calcVal / 100 + ''
      }

      if (['/', '+', '-', '*'].includes(btn)) {
        this.operators = btn
        this.prevCalcVal = this.calcVal
        this.calcVal = ''
      }

      if (btn === "=") {
          this.calcVal = eval(
            this.prevCalcVal + this.operators + this.calcVal
            )
          this.prevCalcVal = ''
          this.operators = null
      }
    }
  },
}
</script>



<template>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background-color: #234;">

    <!-- Calculator Result -->
    <div class="w-full rounded m-1 p-3 text-end lead fw-bold text-white bg-vue-dark">
      {{ calcVal || 0}}
    </div>  

    <!-- Calculator Buttons -->
    <div class="row g-0">
      <div class="col-3" v-for="btn in calcBtns">
        <div 
        class="lead text-white text-center m-1 py-3 bg-vue-dark rounded btn-hover"
        :class="{'bg-vue-green': ['C', '*', '/', '+', '-', '=', '%'].includes(btn)}"
        @click="action(btn)"
          >
          {{ btn }}
        </div>
      </div>
    </div>
  </div>    
</template>


<style scoped>
.bg-vue-dark{
  background: #31475e;
}

.btn-hover:hover{
  cursor: pointer;
  background: #3D5875;
}

.bg-vue-green{
  background: #3fb984 ;
}
</style>
