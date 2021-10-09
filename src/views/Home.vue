<template>
<body>
  <div class= "ndiv">
    <nav><div><h1>Welcome to our Quiz App!</h1></div></nav>
  </div>
   
  <div class="home">
         <div class = "welcome"><img class = "logo1" src="@/assets/science.png" alt=""></div>
         

    <form class = "form1">  
  <label for="items">Items<select @change="changeValue()" id="items" >
    <option value="amount=10" >10</option>
    <option value="amount=15" >15</option>
    <option value="amount=20" >20</option>
    <option value="amount=25" >25</option>
    </select>
  </label></form>


    <form class = "form2">
    <label for="diffi">Difficulty
  <select @change="changeDifficulty()" id="diffi" >
    <option value="difficulty=easy" >Easy</option>
    <option value="difficulty=medium" >Medium</option>
    <option value="difficulty=hard" >Hard</option>
    </select>
    </label></form>


    
    <router-link to="/startquiz"><input type="Submit" value="Start"></router-link>
    </div>
    <!-- </div> -->
</body>
</template>
<script>
export default {
  name: 'Home',
  components: {
  },
  methods: {
    
    changeValue(){
      this.$emit('changeValue')
    },
    changeDifficulty(){
      this.$emit('changeDifficulty')
    }
  }
}
</script>


<style scoped>
body{
  height:100vh;
  width:100vw;
  margin: 0;
  font-family: 'Roboto Condensed', sans-serif;
  background-image: url("../assets/space.jpg");
  background-attachment: fixed;
  background-size: cover;
  position: relative;
  padding:0;
}

.home{
  display: flex;
  flex-direction: column-reverse;
  justify-content: space-around;
  align-items: center;
  background-color: #2f5061b0;
  width: 27vw;
  height: 50vh;
  margin: auto;
  border-radius: 40px;
  margin-top: 80px;
  padding: 50px;
}

.form1{
 order: 2
}

.form2{
 order: 1
}

.welcome{
  order:3;
  color: white;
  
}

form{
  text-align: center;
  font-size: 20px;
}

label{
  display: flex;
  flex-direction: column;
  margin-top: 10px;
  color: white;
  font-weight: bold;
}


input[type=text], select {
  width: 20vw;
  height: 8vh;
  padding: 5px;
  font-size: 20px;
  border: 1px solid #ccc;
  border-radius: 10px; 
  margin-top: 10px;
}


input[type=submit] {
  height: 10vh;
  width: 15vw;
  background-color: #4CAF50;
  color: rgb(10, 10, 10);
  padding: 20px;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  color: white;
  order: 1;
  margin-top: 50px;
  font-size: 24px;
  font-weight: bold;
}


input[type=submit]:hover {
  background-color: #45a049;
}
.ndiv{
  display: flex;
  
}

nav{
  background-color: #189ab4b6;
  width: 90%;
  padding: 20px;
  border-radius: 15px;
  text-align: center;
  margin: auto;
  color:white;
}
h1{
  text-align: center;
  display: flex;
  margin:auto;
}

 .logo1{
    width:80px;
    height:80px;
    margin-right: auto;
    margin-left: auto;
    display: block;
    background-size: cover;
  }



</style>
