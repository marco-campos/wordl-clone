<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <!-- For testing purposes the following line gives us the word -->
   <!--<p>Random word: {{randomWord}}</p> -->
  <button class="button" @click="reloadPage" id="reload">New Word</button>
    <p v-if="!helpDisplay"><a @click="toggleHelp">Click Here</a> For instructions for how to play</p>
    <div v-if="helpDisplay" class="help">Guess the WORDLE in 6 tries. <br>

Each guess must be a valid 5 letter word. Hit the enter button to submit.
<br>
After each guess, the color of the tiles will change to show how close your guess was to the word. <a @click="toggleHelp">Click here to close</a> 
</div>
    <p v-if="showDefintion">Definition: {{definition}}</p>
  <div class="grid-container">
    <div class="grid-item" id="cell1">{{rowOne[0]}}</div>
    <div class="grid-item" id="cell2">{{rowOne[1]}}</div>
    <div class="grid-item" id="cell3">{{rowOne[2]}}</div>
    <div class="grid-item" id="cell4">{{rowOne[3]}}</div>
    <div class="grid-item" id="cell5">{{rowOne[4]}}</div>
    
    <div class="grid-item" id="cell6">{{rowTwo[0]}}</div>
    <div class="grid-item" id="cell7">{{rowTwo[1]}}</div>
    <div class="grid-item" id="cell8">{{rowTwo[2]}}</div>
    <div class="grid-item" id="cell9">{{rowTwo[3]}}</div>
    <div class="grid-item" id="cell10">{{rowTwo[4]}}</div>

    <div class="grid-item" id="cell11">{{rowThree[0]}}</div>
    <div class="grid-item" id="cell12">{{rowThree[1]}}</div>
    <div class="grid-item" id="cell13">{{rowThree[2]}}</div>
    <div class="grid-item" id="cell14">{{rowThree[3]}}</div>
    <div class="grid-item" id="cell15">{{rowThree[4]}}</div>

    <div class="grid-item" id="cell16">{{rowFour[0]}}</div>
    <div class="grid-item" id="cell17">{{rowFour[1]}}</div>
    <div class="grid-item" id="cell18">{{rowFour[2]}}</div>
    <div class="grid-item" id="cell19">{{rowFour[3]}}</div>
    <div class="grid-item" id="cell20">{{rowFour[4]}}</div>

    <div class="grid-item" id="cell21">{{rowFive[0]}}</div>
    <div class="grid-item" id="cell22">{{rowFive[1]}}</div>
    <div class="grid-item" id="cell23">{{rowFive[2]}}</div>
    <div class="grid-item" id="cell24">{{rowFive[3]}}</div>
    <div class="grid-item" id="cell25">{{rowFive[4]}}</div>

    <div class="grid-item" id="cell26">{{rowSix[0]}}</div>
    <div class="grid-item" id="cell27">{{rowSix[1]}}</div>
    <div class="grid-item" id="cell28">{{rowSix[2]}}</div>
    <div class="grid-item" id="cell29">{{rowSix[3]}}</div>
    <div class="grid-item" id="cell10">{{rowSix[4]}}</div>
  </div>
<br/>
  <div class="keyboard">
    <div class="row1">
      <div @click="keyboardButtonPressed" class="keyboard-item" id="Q">Q</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="W">W</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="E">E</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="R">R</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="T">T</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="Y">Y</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="U">U</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="I">I</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="O">O</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="P">P</div>
    </div>
    
    <div class ="row2">
      <div class="keyboard-item" @click="keyboardButtonPressed" id="A">A</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="S">S</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="D">D</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="F">F</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="G">G</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="H">H</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="J">J</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="K">K</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="L">L</div>
    </div>
    
    <div class="row3">
      <div class="keyboard-item" @click="checkWord">Enter</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="Z">Z</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="X">X</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="C">C</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="V">V</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="B">B</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="N">N</div>
      <div class="keyboard-item" @click="keyboardButtonPressed" id="M">M</div>
      <div class="keyboard-item" @click="backspaceButton" id="backspace">Backspace</div>
    </div>
    
  </div>
  
    <br>
    <footer>
        <p class="info">
      Check out my <a href="https://github.com/marco-campos" target="_blank" rel="noopener">github</a> for the code. Credit for the dictionary data: <a href="https://gist.github.com/BideoWego/60fbd40d5d1f0f1beca11ba95221dd38">
BideoWego</a>. Check out <a href="https://www.powerlanguage.co.uk/wordle/">Wordle</a> for the inspiration to the project.</p>
    </footer>
    
  </div>
</template>

<script>
import json from './fiveLetterWords.json'
import text from './dictionaryFive.json'
import websterFive from './websterWordsFive.json'

export default {
  name: 'HelloWorld',
  
  props: {
    msg: String
  },
  data(){
    return {
      rowOne: [],
      rowTwo: [],
      rowThree: [],
      rowFour: [],
      rowFive: [],
      rowSix:[],
      currentRow: 1,
      currentColumn: 1,
      wordSelection: json,
      randomWord: null,
      showDefintion:false,
      randomWordKey: null,
      playerWon: false,
      helpDisplay: false,
      wordBank: text,
      definitions: websterFive,
      definition: null
    }
  },
  mounted(){
    this.getRandomWord()
    
  },
  methods:{
    reloadPage(){
    window.location.reload()
  },
    toggleHelp(){
      this.helpDisplay = !this.helpDisplay
    },
    checkRow(){
      let row = null
      switch(this.currentRow){
        case 1:
          row = this.rowOne
          break
        case 2:
          row = this.rowTwo
          break
        case 3:
          row = this.rowThree
          break
        case 4:
          row = this.rowFour
          break
        case 5:
          row = this.rowFive
          break
        case 6:
          row = this.rowSix
          break
      }
      return row
    },
    checkWord(){
      let row = this.checkRow()
      console.log(row)
      if (row.length !== 5){
        alert("Word is not long enough")
      } else {
        let answer = ""
        for (let i = 0; i < row.length; i++){
          answer += row[i]
        }
        if (answer === this.randomWord){
          alert("You win!")
          this.getDefinition()
          this.playerWon = true
          this.showDefintion = true
          for (let i = 0; i < row.length; i++){
                if (row[i] === this.randomWord[i]){

                  let index = ((i+1)+(this.currentRow-1)*5).toString()
                  let cellselected = "cell" + index
                  const correctCell = document.getElementById(cellselected)
                  correctCell.style["background-color"] = "rgb(102, 255, 153)"
                }}
          
        } else{
          if (this.currentRow ===6){
            alert("You lost :(")
          } else{
            if (!Object.prototype.hasOwnProperty.call(this.wordBank, answer)){
              alert("Word is not in our word bank")
            }
            else{
                for (let i = 0; i < row.length; i++){
                if (row[i] === this.randomWord[i]){
                  this.colorKeyboardCorrect(row[i])
                  let index = ((i+1)+(this.currentRow-1)*5).toString()
                  let cellselected = "cell" + index
                  const correctCell = document.getElementById(cellselected)
                  correctCell.style["background-color"] = "rgb(102, 255, 153)"
                } else if (this.randomWord.includes(row[i]) && row[i] !== this.randomWord[i]){
                  this.colorKeyboardAlmost(row[i])
                  let index = ((i+1)+(this.currentRow-1)*5).toString()
                  let cellselected = "cell" + index
                  const correctCell = document.getElementById(cellselected)
                  correctCell.style["background-color"] = "rgb(255, 255, 153)"
                }
                else{
                  this.colorKeyboardIncorrect(row[i])
                  let index = ((i+1)+(this.currentRow-1)*5).toString()
                  let cellselected = "cell" + index
                  const correctCell = document.getElementById(cellselected)
                  correctCell.style["background-color"] = "rgb(190, 202, 209)"
                }
              }
              alert("Word is not correct")
              this.currentRow += 1
              this.currentColumn =1
            }
            
          }
        }
      }
    },
    highlightCell(){
      //let highlightedRow = this.checkRow()
      let index = ((this.currentColumn)+(this.currentRow-1)*5).toString()
      let cellselected = "cell" + index
      const correctCell = document.getElementById(cellselected)
      correctCell.classList.add('selected')
    },
    removeHighlight(){
      let index = ((this.currentColumn)+(this.currentRow-1)*5).toString()
      let cellselected = "cell" + index
      const correctCell = document.getElementById(cellselected)
      correctCell.classList.remove('selected')
    },
    getDefinition(){
      const currentWord = this.randomWord.toLowerCase()
      console.log(currentWord)
      const defs = Object.keys(this.definitions)
      for (let i = 0; i < defs.length; i++){
        if (currentWord === defs[i]){
          console.log(currentWord, defs[i])
          this.definition = this.definitions[defs[i]]
        }
      }
    },
    colorKeyboardCorrect(letter){
      const correctLetter = document.getElementById(letter)
      correctLetter.style["background-color"] = "rgb(102, 255, 153)"
    },
    colorKeyboardAlmost(letter){
      const correctLetter = document.getElementById(letter)
      correctLetter.style["background-color"] = "rgb(255, 255, 153)"
    },
    colorKeyboardIncorrect(letter){
      const correctLetter = document.getElementById(letter)
      correctLetter.style["background-color"] = "rgb(156, 167, 173)"
    },
    backspaceButton(){
      let row = this.checkRow()
      if (this.currentColumn>1){
        row.pop()
        this.currentColumn -= 1
      }
    },
    keyboardButtonPressed(e){
      //this.removeHighlight()
      let row= this.checkRow()
      
      if (this.currentColumn < 6){
        row.push(e.target.id)
        this.currentColumn += 1

        
        
      } else{
        if (!this.playerWon){
          alert("Too many letters")
        }
        
      }
      
 
    },
    getRandomWord(){
      const values = Object.keys(this.wordSelection)
      const prop = values[Math.floor(Math.random() * values.length)]
      this.randomWordKey = prop
      this.randomWord = prop.toUpperCase()
    }
  },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h3 {
  margin: 1rem 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.button {
  position: relative;
  background-color: #4CAF50;
  border: none;
  font-size: 1.2rem;
  color: #FFFFFF;
  padding: 0.5rem;
  width: 35%;
  text-align: center;
  transition-duration: 0.4s;
  text-decoration: none;
  overflow: hidden;
  cursor: pointer;
  border-radius: 5px;

}

.button:after {
  content: "";
  background: #f1f1f1;
  display: block;
  position: absolute;
  padding-top: 300%;
  padding-left: 350%;
  margin-left: -20px !important;
  margin-top: -120%;
  opacity: 0;
  transition: all 0.8s
}

.button:active:after {
  padding: 0;
  margin: 0;
  opacity: 1;
  transition: 0s
}

.info{
  font-size: 0.7rem
}
.grid-container {
  display: grid;
  grid-gap: 0.3rem;
  justify-content: center;
  grid-template-columns: repeat(5, 4rem);
  grid-template-rows: repeat(6, 4rem);
  background-color: #2196F3;
  padding: 0.4rem;
  width: 22rem;
  margin: 0 auto;
  border-radius: 3px;
  

  
}
.grid-item {
  display: flex;
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  font-size: 1.5rem;
  justify-content: center;
  align-items: center;
  border-radius: 3px;

}
.grid-item.selected{
 border: 2px solid purple;
}
.keyboard {
  display: grid;
  grid-template-columns: auto ;
  background-color: #2196F3;
  padding: 10px;
  border-radius: 5px;

  
}
.keyboard-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  font-size: 1rem;
  text-align: center;
}
.row1 {
  display: grid;
  grid-template-columns: auto auto auto auto auto auto auto auto auto auto ;
  background-color: #2196F3;
  padding: 10px;
}
.row2 {
  display: grid;
  grid-template-columns:  auto auto auto auto auto auto auto auto auto ;
  background-color: #2196F3;
  padding: 10px;
}
.row3 {
  display: grid;
  grid-template-columns:  auto auto auto auto auto auto auto auto auto ;
  background-color: #2196F3;
  padding: 10px;
}
.help{
  padding-bottom: 1rem
}

@media all and (min-width:0px) and (max-width: 650px) {
  html, body {
    max-width: 100%;
    overflow-x: hidden;
}
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto auto;
  grid-template-rows: auto auto auto auto auto;
  background-color: #2196F3;
  padding: 0.4rem;
  width:75%;
  margin: 0 auto
  
}
.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 1rem;
  font-size: 1.5rem;
  text-align: center;

}
  .keyboard {
  display: grid;
  grid-template-columns: auto ;
  background-color: #2196F3;
  padding: 0;

  
}
  .keyboard-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 0.5rem;
  font-size: 0.8rem;
  text-align: center;
  }
}


</style>
