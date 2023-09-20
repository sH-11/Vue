<template>
    <div style="max-width:400px;margin: 50px auto;background:#555" class="p-3">

        <!--Calculator result-->
        <div class="w-full rounded m-1 p-3 text-end lead font-weight-bold text-white bg-vue-dark">
            {{calculatorValue || 0}}
        </div>
         <!--calvulator buttons-->
        <div class="row no-gutters">
                <div class="col-3" v-for="n in calculatorElements" :key="n">
                    <div class="lead text-white text-center m-1 p-3 bg-vue-dark rounded hover-class"
                    :class="{'bg-green':['C','*','/','+','-','%','='].includes(n)}" @click="action(n)">
                        {{n}}
                    </div>

                </div>
        </div>

    </div>
</template>

<script>
    export default {
        name:'CalcuLator',
        data(){
            return{
                calculatorValue:'',
                calculatorElements:['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
                operator:null,
                previousCalculatorValue:'',
            }
        },
        methods:{
            action(n){
                /*append value --> click on value*/
            if(!isNaN(n)||n==='.'){
                this.calculatorValue += n + '';
              }

              /*clear value*/

              if(n==='C'){
                  this.calculatorValue='';
              }
              /*% condition*/
              if(n==='%'){
                  this.calculatorValue=this.calculatorValue/100 + '';
              }

              if(['/','*','+','-'].includes(n)){
                  this.operator=n;
                  this.previousCalculatorValue=this.calculatorValue;
                  this.calculatorValue='';

              }
              if(n ==='='){
                  this.calculatorValue=eval(
                      this.previousCalculatorValue + this.operator + this.calculatorValue
                  );
                  this.previousCalculatorValue='';
                  this.operator=null;
              }

            }
        }
    }
</script>

<style scoped>
.bg-vue-dark{
    background:grey;
}
.hover-class:hover{
    background:rgb(173, 250, 173);
    cursor: pointer;
}
.bg-green{
    background: rgb(63, 150, 63);
}

</style>