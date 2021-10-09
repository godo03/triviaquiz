<template>
<body>
   <div id = "app">
     <nav><h1>Review Page</h1>
     <div class = "welcome"><img class = "logo1" src="@/assets/science.png" alt=""></div>
     <h2>Your Score: {{reviewScore}} / {{reviewItems}}</h2></nav>

<table id = "data">
   <tr> 
            <td>Question</td>  
            <td>Correct Answer</td> 
            <td> Your Answer</td> 

         </tr>
  <tr v-for="question, index in reviewQ" :key="index">
    <td>{{question.question}}</td>
    <td class="correctanswer">{{question.correct_answer}}</td>
    <td v-bind:class="[isitCorrect(question.correct_answer, reviewAns[index] 
    ) ? 'correctanswer'  : '']">{{reviewAns[index]}}</td>
  </tr>
</table>

   
<div class = "buttons2">
<router-link to="/startquiz"><button class = "btnP" @click="$emit('resetUserAns')"> </button></router-link>
<router-link to="/"><button class = "btnH" @click="$emit('changeUrl')"></button></router-link>
                       
</div>
</div>
</body>

  
  
</template>

<script>


export default {
     props: {
    reviewQ: Array,
    reviewAns: Array,
    reviewScore: String,
    reviewItems: String
    


  },
  data () {
    return {
     array: this.reviewAns, 
     

     
    }
  },
  methods: {
  isitCorrect(cr, ua){
      return cr == ua;
      
    }
  },

}
</script>

<style>
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

button:hover{
  background-color: #4f6fa093;
  color: white;
}
.correctanswer{
  color: rgb(12, 133, 12);
}

.wronganswer{
  color: rgb(185, 74, 22);
}



#data {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  max-width: 100%;
  text-align: left;
  margin-top: 20px;
  font-weight:bold ;
  font-size: 18px;
  border-top-style: solid;
  border-bottom-style: solid;
  border-color: black;
  margin-left: auto;
  margin-right: auto;
}

#data td, #data th {
  border: 1px solid #ddd;
  padding: 12px;
}

#data tr{
  background-color: #cccacae8;
  } 

#data tr:hover {background-color: rgba(167, 167, 167, 0.904);

}

#data tr{ max-width: 50px;}


nav{
  background-color: rgba(57, 196, 154, 0.712);
  position: relative;
  padding: 15px;
  border-radius: 15px;
  display: flex;
  flex-direction: row;
  max-width: 90vw;
  justify-content: space-around;
  margin:auto;
}

h1{
  order: 1;
}

.welcome{
  order: 2;
}

h2{
  order: 3;
}



.logo1{
   
    width:80px;
    height:80px;
    background-size: cover;
  }

button{
    border-radius: 50px;
}

.buttons2{
margin-top: 8px;
background-color: rgba(0, 0, 0, 0.445);
}



.btnP{
    order:1;
    background:url("../assets/restart2.png") no-repeat;
    cursor:pointer;
    border:none;
    width:80px;
    height:80px;
    background-size: cover;
}
.btnH{
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