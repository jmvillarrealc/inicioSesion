<template>
  <div class="home">
    <div>
      <div>
        <div class="wrapper fadeInDown">
          <!-- Titulo -->
          <h6>{{ titlePrin() }}</h6>
          
          <div id="formContent">

            <!-- Icono -->
            <div class="fadeIn first">
              <img src="@/assets/logo-big.png" id="icon" alt="User Icon" />
            </div>
            <br>
            <h7>{{ subtitle() }}</h7>
            

            <!-- Formato  -->
            <form v-on:submit.prevent="login">
              <input type="text" id="email" class="fadeIn second" name="email" placeholder="email@example.com" v-if="type!=1" v-model="email">
              <p v-show="correoOk">{{ msgEmail }}</p>
              <input type="text" id="login" class="fadeIn second" name="login" placeholder="Usuario" v-if="type!=2" v-model="usuario">
              <p v-show="usuarioOk">{{ msgUsuario }}</p>
              <input type="text" id="password" class="fadeIn third" name="login" placeholder="Password" v-if="type!=2" v-model="password">
              <p v-show="usuarioOk">{{ msgUsuario }}</p>e 
              
              <div class="btnAll">
                <input  :disabled="validateForm" @click="type=0" type="submit" class="fadeIn fourth" value="Solicitar Registro">
                <input @click="type=1" type="button" class="fadeIn fourth" value="Regresar a Login">
              </div>
            </form>

            <!-- link Para Recuperar Passowrd -->
            <div id="formFooter">
              <a class="underlineHover" @click="type=2" href="#">Forgot Password?</a>
            </div>

          </div>
        </div>
      </div>
    </div>
    
      
  </div>
</template>

<script>
// @ is an alias to /src
//import axios from 'axios';
export default {
  name: 'HomeView',
  components: {

  },
  data: function() {
    return{
      email:'',
      usuario:'',
      password:'',
      msgEmail : '',
      msgUsuario : '',
      msgPassword : '',
      type :0, //0 = login, 1= Registro, 2= Recuperar contraseña,
      title: 0, //0= login, 1= Registro, 2= Recuperar contraseña,
    }
  }, // data
  methods:{
      correoOk : function(){
      const emailRegex = new RegExp(/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/);
      if(!emailRegex.test(this.email)) {
        this.msgEmail="Formato de email inválido"
      }else{
        this.msgEmail="Formato de email es correcto"  
      }
    },//correoOK
    usuarioOk : function(){
      if(this.usuario.length < 4){
        this.msgUsuario ="Formato de usuario inválido"
      }else{
        this.msgUsuario = "Formato de usuario correcto"
      }
    },//usuarioOK
    passwordOk : function(){
      const passwordRegex = new RegExp(/^(((?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,}))$/);
      if(!passwordRegex.test(this.password)){
        this.msgPassword = "Formato de password inválido"
      }else{
        this.msgPassword = "Formato de password válido"
      }
    },//passwordOk
    comprobacion : function(){
      this.correoOk()
      this.usuarioOk()
      this.passwordOk()
    },//comprobacion
    subtitle(){
      return (this.type==0)?'Introduce los datos que se te solicitan':(this.type==1)?' Iniciar Sesión':'Introduce el correo electrónico con el que te registraste en el sistema para recuperar tu cuenta';
    },
    titlePrin(){
      return  (this.type==0)?'Forma de registro':(this.type==1)?' Iniciar Sesión':'Regeneración de clave';
  
     }
    

      
    //   axios.post('http://solodata.es/auth',json).then(data =>{
    //     console.log(data);
    //   })
    // }//methods
  },
}//export default
</script>

<style scoped>

/* BASIC */

html {
  background-color: #56baed;
}

body {
  font-family: "Poppins", sans-serif;
  height: 100vh;
}

a {
  color: #92badd;
  display:inline-block;
  text-decoration: none;
  font-weight: 400;
}

h2 {
  text-align: center;
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  display:inline-block;
  margin: 40px 8px 10px 8px; 
  color: #cccccc;
}
h6{
  color: #fff;
}
h7{
  color: #fff;
}



/* STRUCTURE */


.wrapper{
  background-image: linear-gradient(0deg, rgba(108, 113, 164, 0.8), rgba(0,0,0,0.8)), url(@/assets/fondo.jpg);
	background-size:cover;
	background-position:center center;
	width:100%;
	height:100vh;
  display: flex;
  align-items: center;
  flex-direction: column; 
  justify-content: center;
  width: 100%;
  min-height: 100%;
  padding: 20px;
}

#formContent {
  -webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  border: .2px solid #0d0d0d;
  padding: 30px;
  width: 90%;
  max-width: 450px;
  position: relative;
  padding: 0px;
  -webkit-box-shadow: 0 30px 60px 0 rgba(0,0,0,0.3);
  box-shadow: 0 30px 60px 0 rgba(0,0,0,0.3);
  text-align: center;
}

#formFooter {
  color: #fff;
  padding: 25px;
  text-align: center;
  -webkit-border-radius: 0 0 10px 10px;
  border-radius: 0 0 10px 10px;
}

.btnAll{
  display:flex;
  justify-content: center;
  align-items: center;
  padding: 30px 80px;  
}



/* TABS */

h2.inactive {
  color: #cccccc;
}

h2.active {
  color: #0d0d0d;
  border-bottom: 2px solid #5fbae9;
}



/* FORM TYPOGRAPHY*/

input[type=submit], input[type=reset]  {
  background-color: #1b5e12;
  border: none;
  color: white;
  padding: 15px 28px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  text-transform: uppercase;
  font-size: 13px;
  -webkit-box-shadow: 0 10px 30px 0 rgba(136, 138, 139, 0.4);
  box-shadow: 0 10px 30px 0 rgba(130, 131, 131, 0.4);
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
  margin: 5px 20px 40px 20px;
  -webkit-transition: all 0.3s ease-in-out;
  -moz-transition: all 0.3s ease-in-out;
  -ms-transition: all 0.3s ease-in-out;
  -o-transition: all 0.3s ease-in-out;
  transition: all 0.3s ease-in-out;
}
input[type=button]  {
  background-color: #afa120;
  border: none;
  color: white;
  padding: 15px 28px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  text-transform: uppercase;
  font-size: 13px;
  -webkit-box-shadow: 0 10px 30px 0 rgba(95,186,233,0.4);
  box-shadow: 0 10px 30px 0 rgba(95,186,233,0.4);
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
  margin: 5px 20px 40px 20px;
  -webkit-transition: all 0.3s ease-in-out;
  -moz-transition: all 0.3s ease-in-out;
  -ms-transition: all 0.3s ease-in-out;
  -o-transition: all 0.3s ease-in-out;
  transition: all 0.3s ease-in-out;
}

input[type=button]:hover, input[type=submit]:hover, input[type=reset]:hover  {
  background-color: #5b5d5e;
}

input[type=button]:active, input[type=submit]:active, input[type=reset]:active  {
  -moz-transform: scale(0.95);
  -webkit-transform: scale(0.95);
  -o-transform: scale(0.95);
  -ms-transform: scale(0.95);
  transform: scale(0.95);
}

input[type=text] {
  border: none;
  color: #ffffff;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 5px;
  width: 85%;
  border-bottom:2px solid #fff ;
  -webkit-transition: all 0.5s ease-in-out;
  -moz-transition: all 0.5s ease-in-out;
  -ms-transition: all 0.5s ease-in-out;
  -o-transition: all 0.5s ease-in-out;
  transition: all 0.5s ease-in-out;
  -webkit-border-radius: 5px 5px 5px 5px;
  border-radius: 5px 5px 5px 5px;
  background-color: rgba(0,0,0,0);
}

input[type=text]:focus {
  border-bottom: 2px solid #5fbae9;
}
input[type=text]:error {
  border-bottom: 2px solid #5fbae9;
}
input[type=text]:placeholder {
  color: #cccccc;
}



/* ANIMATIONS */

/* Simple CSS3 Fade-in-down Animation */
.fadeInDown {
  -webkit-animation-name: fadeInDown;
  animation-name: fadeInDown;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}

@-webkit-keyframes fadeInDown {
  0% {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
  100% {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}

@keyframes fadeInDown {
  0% {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
  100% {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}

/* Simple CSS3 Fade-in Animation */
@-webkit-keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
@-moz-keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
@keyframes fadeIn { from { opacity:0; } to { opacity:1; } }

.fadeIn {
  opacity:0;
  -webkit-animation:fadeIn ease-in 1;
  -moz-animation:fadeIn ease-in 1;
  animation:fadeIn ease-in 1;

  -webkit-animation-fill-mode:forwards;
  -moz-animation-fill-mode:forwards;
  animation-fill-mode:forwards;

  -webkit-animation-duration:1s;
  -moz-animation-duration:1s;
  animation-duration:1s;
}

.fadeIn.first {
  -webkit-animation-delay: 0.4s;
  -moz-animation-delay: 0.4s;
  animation-delay: 0.4s;
}

.fadeIn.second {
  -webkit-animation-delay: 0.6s;
  -moz-animation-delay: 0.6s;
  animation-delay: 0.6s;
}

.fadeIn.third {
  -webkit-animation-delay: 0.8s;
  -moz-animation-delay: 0.8s;
  animation-delay: 0.8s;
}

.fadeIn.fourth {
  -webkit-animation-delay: 1s;
  -moz-animation-delay: 1s;
  animation-delay: 1s;
}

/* Simple CSS3 Fade-in Animation */
.underlineHover:after {
  display: block;
  left: 0;
  bottom: -10px;
  width: 0;
  height: 2px;
  background-color: #56baed;
  content: "";
  transition: width 0.2s;
}

.underlineHover:hover {
  color: #0d0d0d;
}

.underlineHover:hover:after{
  width: 100%;
}



/* OTHERS */

*:focus {
    outline: none;
} 

#icon {
  width:30%;
}

</style>