<template>
<div class="banner">
<div class="caculator">
      <div class="display">{{current}}</div>
     <div class="btn">CE</div>
     <div class="btn " @click="btn_clear">C</div>
     <div class="btn" @click="btn_Del">Del</div>
     <div class="btn operator" @click="division()">/</div>
     <div class="btn" @click="append(7)">7</div>
     <div class="btn" @click="append(8)">8</div>
     <div class="btn" @click="append(9)">9</div>
     <div class="btn operator" @click="multiplication">X</div>
     <div class="btn" @click="append(4)">4</div>
     <div class="btn" @click="append(5)">5</div>
     <div class="btn" @click="append(6)">6</div>
     <div class="btn operator" @click="subtraction">-</div>
     <div class="btn" @click="append(1)">1</div>
     <div class="btn" @click="append(2)">2</div>
     <div class="btn" @click="append(3)">3</div>
     <div class="btn operator" @click="summation">+</div>
     <div class="btn " @click="changeNegative">+/-</div>
     <div class="btn" @click="append(0)">0</div>
     <div class="btn" @click="dot" > .</div>
     <div class="btn operator" @click="equal">=</div>
</div>
  </div>
  
</template>

<script>
export default {
    name: 'caculator',
    data(){
        return{
            preCurrent:null,
            current:'0',
            operator:null,
            isCheckOperator:false
        }
    },
    methods:
    {
        btn_clear()
        {
            this.current='0';
        },
        btn_Del(){
            this.current=this.current.slice(0,-1);
            if(this.current==='')
                this.current='0';
        },
        append(number)
        {
            if(this.current[0]==='0'||this.isCheckOperator)
            {
                this.current='';
                this.isCheckOperator=false;
            }
            this.current=this.current+number;
        },
        setPreCurrent()
        {
            this.preCurrent=this.current;
           
            this.isCheckOperator=true;
        },
       division(){
           this.operator=(a,b)=>a/b;
           this.setPreCurrent();
       },
       subtraction()
       {
           this.operator=(a,b)=>a-b;
           this.setPreCurrent();
       },
       summation()
       {
           this.operator=function(a,b)
           {
               return a+b;
           }
           this.setPreCurrent();
       },
       multiplication()
       {
           this.operator=(a,b)=>a*b;
           this.setPreCurrent();
           console.log(this.operator);
       }
       ,
       changeNegative()
       {
           if(this.current!=='0')
           {
               this.current=(parseFloat(this.current)*(-1)).toString();
           }
       },
       dot()
       {
           if(this.current.indexOf('.')==-1)
           {
               this.current+='.';
           }
       }
       ,
       equal()
       {
           this.current=this.operator(
               parseFloat(this.preCurrent),
               parseFloat(this.current)
           ).toString();
       }

    }
}
</script>

<style>
    .banner{
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .caculator{
        max-width: 500px;
        min-width: 300px;
        display: grid;
        grid-template-columns: repeat(4,1fr);
        grid-auto-rows:minmax(50px,auto);
        padding:20px;
    }
    .display{
        grid-column: 1/5;
        width: 100%;
        height: 100%;
        background: silver;
        display: flex;
        justify-content:center;
        align-items: center;
        font-family: Arial, Helvetica, sans-serif;
        font-size:1.5em; 
       
    }
    .btn{
         display: flex;
        justify-content: center;
        align-items: center;
        border: 1px solid black;
        transition: all .5s ease;
        cursor: pointer;
    }
    .operator{
        background:orange;
    }
    .btn:hover{
        background: black;
        color:white;
    }
</style>