<template>

  <div id="app">
<body>
<div class = "panel">
<div v-if="index < count">
    <panel class = "p1">
<div class = "qno"><h1>Question No:{{index + 1}}/{{count}}</h1></div>
<div class = "qh"><p> <strong>Your Score:
    <span>{{ score }}</span> 
<br><span> {{percentScore()}}% </span></strong>
</p></div>
<div class = "timer" >
<b-card-text>
<span style="font-size: 40px;"><strong>{{countDown}} </strong></span>
</b-card-text>
</div>
</panel>
                        <div class = "pqd">
                        <p class = "pq">
                            {{questions[index]['question'] }} 
                        </p>
                        </div>




<div class="choicestab"  :key="answer" v-for="answer in choices[index]">
    <button class = "btnchoice focus" :value="answer" @click="userPick($event)">{{answer}}</button>
  </div>
   

 <div class ="earlybuttons">
<button class = "btnEp" @click="resetQuiz()"> </button>
<router-link to="/"><button class = "btnEh" @click="$emit('changeUrl')"> </button></router-link>
<button class="btnEn" :disabled="selectedAnswer == ''" @click="submitAnswer(selectedAnswer)"> </button>


                           
</div>                       
</div>

<div v-else>
    <div class = "welcome"><img class = "logo1" src="@/assets/science.png" alt=""></div>
    <h1>Results</h1>

<div class = "scoreR">
<p class = "pblack"><strong> Your Score: {{ score }} / {{count}} <br><br>
<span> {{percentScore()}}% </span></strong>
</p>
                            
</div>

<div class ="buttons">
    
<button class = "btnP" @click="resetQuiz()"></button>
<router-link to="/"><button class = "btnH" @click="$emit('changeUrl')" /></router-link>
<router-link to="/review"><button class = "btnR" @click="$emit('setQuestions', questions), $emit('setScore', score), $emit('setNoOfItems', count)"> </button></router-link>
                          
</div>  


</div>                      
</div>
</body>   

</div> 
</template>
<script>

import axios from 'axios'

export default {
  name: 'App',
  components: {
     
  },
  props: {
    urlLink: String,
  },
data() {
        return {
            index: 0,
            selectedAnswer: '',
            score: 0,
            count: 1,
            questions: [],
            choices: [],
            ulink: this.urlLink,
            countDown : 10,
            timer:null,
            
    
         
        }
    },
  async created() {
      
    try {
        const response = await axios.get(this.ulink)
        this.questions = response.data.results;
        let array = this.questions
        this.count = array.length
        this.choices = this.assignAnswers(this.questions);
        this.countDownTimer();
        }catch (e) {
        this.errors.push(e)
        }
        },
    methods: {
        percentScore(){
        return Math.floor((this.score / this.count) * 100)
        },
        submitAnswer(item){
            clearTimeout(this.timer);
            let nextQuestion = this.currentQuestion + 1;
            if(this.selectedAnswer == this.questions[this.index].correct_answer)
                this.score++
                this.index++
                this.selectedAnswer = ''
           if(this.selectedAnswer < this.questions.length){
        this.countDown = 10;
        this.countDownTimer();
        } 
        if(nextQuestion < this.questions.length){
            this.currentQuestion = nextQuestion;
        }
        else{      
        this.showScore = true
        this.$emit('onUserAnswer', item)  
        }

        },
       
        countDownTimer() {
                if(this.countDown >= 0) {
                    this.timer = setTimeout(() => {
                        this.countDown -= 1
                        this.countDownTimer()
                    }, 1000)
                }
                else if(this.selectedAnswer == ''){
                    this.submitAnswer('No Answer')
                }
                else{
                    this.submitAnswer(this.selectedAnswer)
                }
            },
        userPick(e) {
        this.selectedAnswer = e.target.value
        },
        nextQuestion() {
            this.index++
            this.selectedAnswer = '' 
        },
        showResults() {
            this.index++
        },
        resetQuiz() {
            clearTimeout(this.timer)
            this.index = 0
            this.selectedAnswer = ''
            this.score = 0
            this.countDown = '10';
            this.countDownTimer()
            this.currentQuestion = 0;
            this.$emit('resetUserAns')
        },
        assignAnswers(que){
        let i = 0;
        var ch =[];
        while(i < que.length){
        ch[i] = que[i].incorrect_answers;
        ch[i].push(que[i].correct_answer);
        ch[i] = this.shuffleAnswers(ch[i]);
        i++;
            }
        return ch;
        },
        shuffleAnswers(arr){
        let j, x, i;
        for (i = arr.length - 1; i > 0; i--){
        j = Math.floor(Math.random() * (i + 1));
        x = arr[i];
        arr[i] = arr[j];
        arr[j] = x;  
        }
        return arr;
        },
    } 
}
</script>





<style scoped>
body{
    padding: 0;
    margin: 0;    
    width:100vw;
    height:100vh;  
    font-family: 'Asap', sans-serif;
    background-image: url("../assets/space.jpg");
    background-attachment: fixed;
    background-size: cover;
    position: relative;
     
}
p{
    color: white;
}

.panel{
    min-height: 80vh;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: 90%;
    margin:auto;
    position: relative;
}
.p1{
display: flex;
flex-direction: row;

align-items: center;
justify-content: space-between;
background-color: #fcb5acdc;
border-bottom-left-radius: 20px;
border-bottom-right-radius: 20px;
}


.qh{
    order: 1;
    padding: 20px;
    font-size: 18px;
}

.qno{
    order: 2;
    margin:auto;
        
}
.timer{
    order: 3;
    padding-right: 50px;   
    
    
}


.choicestab{
    display: flex;
    justify-content: space-around; 
    margin-top: 10px;
    padding: 5px;
    width: 80vw;
    height: 10vh;
   
}


.btnchoice{
    margin-top: 20px;
    padding: 10px;
    border-radius: 20px;
    margin-right: 10px;   
    width: 20vw;
    height: 12vh;
    font-size: 18px;
    display: inline-block;
    vertical-align: middle;
    background-color: #f4eae6;
    
    
}
button:hover{
background-color: #b6e2d3c4;
color: white;
}

.next{
    width: 70px;
    height: 50px;
    border-radius: 20px;
}



button{
    border-radius: 50px;
}

.buttons{
    margin-top: 20px;
}

.btnP{
    order:1;
    background:url("../assets/restart.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
}
.btnH{
    order:2;
    background:url("../assets/home.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
    margin-left: 20px;
    margin-right: 20px;
   
   
}

.btnR{
    order:3;
    width: 10vw;
    height: 12vh;
    background:url("../assets/review.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
}



.scoreR{
background-color: #4296a0d3;
border-radius: 50px;
padding: 50px;
font-size: 30px;
margin-top: 0;

}

.pblack{
color: white;
}

h1{
    margin-top: 0;
    color: white;
   
}

.pq{
    display: flex;
    color: white;
    align-items: center;
    justify-content: center;
    font-size: 20px;

     
}

.pqd{
    width: 50vw;
    background-color: #05435ec0;
    color: black;
    padding: 10px;
    border-radius: 20px;
    margin: auto;  
    text-align: center;
    margin-top: 20px;  
}

.focus:focus {
  color: black;
  background-color: #b6e2d3;

}

.earlybuttons{
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    margin-top: 50px;
   margin-right: 20px;
    

}

.btnEp{
    order:3;
    background:url("../assets/restart2.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
}
.btnEn{
    order:1;
    background:url("../assets/share.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
    margin-left: 20px;
    margin-right: 20px;
}

.btnEh{
    order:2;
    background:url("../assets/home2.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
    margin-left: 20px;
    margin-right: 20px;
   
}

</style>