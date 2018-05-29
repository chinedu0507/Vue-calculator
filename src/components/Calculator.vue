<!-- The Calculator -->
<template>
  <div id="Calculator">
    <!-- calculator display div -->
    <div id="display">
      {{display}}
    </div>

    <!-- Buttons div -->
    <div class="buttons">
      <div class="button-row" v-for="row in buttonRows">
        <div
          @click="buttonClick(button)"
          :class="{operator: button.type == 'operator'}"
         class="button" v-for="button in row">
          {{button.text}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default{
    name: 'Calculator',
    methods: {
      buttonClick: function(button){
        if(button.type == 'number'){
          if(this.previousValue === null){
            this.previousValue = Number(this.display);
            // clear the display after an operator has been pressed
            this.display = '';
          }

          // clear zero once a number is pressed and also
          if(this.display === '0' ){
            this.display = '';
          }

          // make sure that you cannot have more than one zero
          if(this.display === '0' && button.text == '0') return;

          // Conditional to ensure that decimal point is only used once
          if(button.text == '.' && this.display.includes('.')) return;

          // the includes() function is used to check if what is passed in the function is included in whatever string is calling it. ie

          // var str = "Hello world";
          // var n = str.includes("world");
          //
          // this will return true

          // display the numbers on the screen
          this.display += button.text;
        } else if (button.text == 'AC') {
          this.display = '0';
        } else if (button.text == 'C') {
          // This clears one number from what is inputed. 0 indicates the starting number
          // -1 signifies the end. so slice(0,-1) means extract the first element to the
          // number just before the end (because the end is up to and not including!)
          this.display = this.display.slice(0,-1);
        }else if (button.text == '+/-') {
            this.display *= -1;
          }
          // Check for equals sign
          else if(button.text == '='){
            // adding '+' before a string number parses it to a number instead of doing Number()

            // operations here is an object but can be accessed as an array (named indexes)
            this.display = this.operations[this.currentOperator](+this.previousValue, +this.display);
            this.currentOperator = '';
          } else if (button.type == 'operator') {
            // if currentOperator exists carry out operations before carrying out subsequent functions

            if(this.currentOperator){
              this.display = this.operations[this.currentOperator](+this.previousValue, +this.display);
            }
            this.previousValue = null;
            // Assigning the currentOperator the operator button that was clicked
            this.currentOperator = button.text;
          }
        }
    },
    data(){
      return{
        display: '0',
        previousValue: '',
        currentOperator: '',
        operations: {
          '+': (a,b) => a + b,
          '-': (a,b) => a - b,
          'x': (a,b) => a * b,
          '/': (a,b) =>  a / b,
          '%': (a,b) => b * 0.01
        },
        buttonRows:[
          [{
            text: 'AC',
            type: 'operator'
          },{
            text: 'C',
            type: 'operator'
          },{
            text: '%',
            type: 'operator'
          },{
            text: '/',
            type: 'operator'
          }],
          [{
            text: '7',
            type: 'number'
          },{
            text: '8',
            type: 'number'
          },{
            text: '9',
            type: 'number'
          },{
            text: 'x',
            type: 'operator'
          }],
          [{
            text: '4',
            type: 'number'
          },{
            text: '5',
            type: 'number'
          },{
            text: '6',
            type: 'number'
          },{
            text: '-',
            type: 'operator'
          }],
          [{
            text: '1',
            type: 'number'
          },{
            text: '2',
            type: 'number'
          },{
            text: '3',
            type: 'number'
          },{
            text: '+',
            type: 'operator'
          }],
          [{
            text: '+/-',
            type: 'operator'
          },{
            text: '0',
            type: 'number'
          },{
            text: '.',
            type: 'number'
          },{
            text: '=',
            type: 'operator'
          }]
        ]
      }
    }
  }
</script>

<style scoped>
  #Calculator{
    margin: 0 auto;
    /* width: 320px; */
    width: 25%;
    height: auto;
    /* height: 530px; */
    background: #999;
    border-radius: 5px;
    opacity: 0.8;
    /* background: #f4f4f4; */
    font-family: Helvetica;
  }

  #display{
    background: #888;
    box-sizing: border-box;
    text-align: right;
    border-radius: 5px;
    padding-top: 35px;
    padding-right: 4px;
    height: 65px;
    color: #fff;
    font-size: 22px;
  }

  .button-row{
    display: flex;
    justify-content: space-around;
  }

  .button{
    display: inline-block;
    /* background: #f4f4f4; */
    background: #fff;
    color: #000;
    box-sizing: border-box;
    font-size: 19px;
    margin: 1.5px;
    padding: 6px;
    height: 30px;
    width: 100%;
  }

  .button:hover{
    background: lightgrey;
  }

  .button:active{
    background: lightgrey;
  }

  .operator{
    background: skyblue;
    color: #000;
  }

  .operator:hover{
    background: #519dbb;
  }

  .operator:active{
    background: #519dbb;
  }
</style>
