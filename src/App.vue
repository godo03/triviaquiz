<template>
<div>

   
    <router-view @changeValue="changeQvalue()"
                 @changeDifficulty="changeDiff()"
                 @changeUrl="changeLink()" :urlLink="link"
                 @onUserAnswer='userAnswerss'
                 @resetUserAns='resetAnswers'
                 @setQuestions='setQ'
                 @setScore='setS'
                 @setNoOfItems='setNoI'
                 :reviewQ='questionset'
                 :reviewAns='userAnswer'
                 :reviewScore='userScore'
                 :reviewItems='numberOfItems'
                 >
    </router-view>  

</div>
  
</template>
<script>
export default {
  name: 'Main',
  components:{  
  },
  data(){
    return{
      items: "amount=10",
      link: 'https://opentdb.com/api.php?amount=10&category=17&difficulty=easy&type=multiple',
      diffi: 'difficulty=easy',
      userAnswer: [],
      questionset: [],
      userScore: "",
    }},
  methods: {
    setQ(value){
      this.questionset = value
    },
    setS(value){
      this.userScore = value
    },
    setNoI(value){
      this.numberOfItems = value
    },
    resetAnswers(){
      this.userAnswer = []
    },
    userAnswerss(value){
      this.userAnswer.push(value)
    },
    
    changeLink() {
      this.link = 'https://opentdb.com/api.php?amount=10&category=17&difficulty=easy&type=multiple',
      this.items = "amount=10",
      this.diffi = 'difficulty=easy'
      this.userAnswer = []
        },
    changeQvalue(){
     this.items = document.getElementById("items").value;
     this.link = 'https://opentdb.com/api.php?'+ this.items +'&category=17&'+this.diffi+'&type=multiple' 
    },
    changeDiff(){
    this.diffi = document.getElementById("diffi").value;
    this.link = 'https://opentdb.com/api.php?'+ this.items +'&category=17&'+this.diffi+'&type=multiple'
    },
  }
}
</script>
<style>
#app {
  font-family: 'Asap', sans-serif;
  
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
