<template>
  <div id="app" class="container mt-5">
         <h1>Form Vue</h1>
 <transition name="slide-fade">
   
        <div v-if="!submitted">

          <custom-input v-model="name" 
                        type="text"                    
                        @getvalidation="GetValidationMethod"
                        placeholder="Your name"
                        label="Name"> </custom-input>

          <custom-input v-model="mobile" 
                        type="number"                    
                        @getvalidation="GetValidationMethod"
                        placeholder="Your mobile number"
                        label="Mobile"> </custom-input>

          <custom-input v-model="postcode"
                        type="number"                    
                        @getvalidation="GetValidationMethod"
                        placeholder="Your postcode"
                        label="Postcode"> </custom-input>

          <custom-input v-model="email" 
                        type="email"             
                        @getvalidation="GetValidationMethod"
                        placeholder="Your email"
                        label="Email"> </custom-input>

          <custom-input v-model="password" 
                        type="password"            
                        @getvalidation="GetValidationMethod"
                        placeholder="Your password"
                        label="Password"> </custom-input>

          <custom-input v-model="confirmation" 
                        type="password"             
                        @getvalidation="GetValidationMethod"
                        placeholder="Repeat passowrd"
                        label="Confirmation"> </custom-input>

        <div class="form-group mt-5"><a type="submit" @click="SubmitForm" class="btn btn-lg btn-dark">Submit</a>  </div>
        </div>  
        <div v-else class="alert alert-success" role="alert">
          <h5>Thank you</h5>
         <p>Your validation was a success!</p>
        </div>
        </transition>
    </div>  
</template>

<script>
import CustomInput from './components/CustomInput.vue'

export default {
  name: 'App',
  components: {
    CustomInput
  },
  data() {
        return {
          name: "",
          validName: false,
          mobile: "",
          validMobile: false,
          postcode: "",
          validPostcode: false,
          email: "",
          validPostcode: false,
          password:"",
          validPassword:false,
          confirmation:"",
          validConfirmation:false,
          submitted: false,
          // validated: false
    }
  },
    methods: {
        resetInput() {
        this.name = "";
        this.mobile = "";
        this.postcode = "";
        this.email = "";
        this.password = "";
        this.confirmation = "";
      },
      GetValidationMethod(valid, label){
        // que es valid? 
        switch(label){
          case 'Name':
            if(valid === true) {
              this.validName = true
            } 
            break;
          case 'Mobile':
            if(valid === true) {
              this.validMobile = true
            }
            break; 
          case 'Postcode':
              if(valid === true) {
            this.validPostcode = true
            }
          break; 
          case 'Email':
            if(valid === true) {
              this.validEmail = true
              }
            break;
            case 'Password':
              if(valid === true) {
                this.validPassword = true
                }
              break;
        }
      },
      SubmitForm(e){   
        this.GetValidationMethod();
            if( this.validName && this.validMobile && this.validPostcode && this.validEmail && this.validPassword ){
              console.log('submitted')
              this.submitted = true;
              this.resetInput();
            } else {
              this.submitted = false;
              e.preventDefault;
              alert('Form has errors')
            }
      }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400&display=swap');
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: 'IBM Plex Mono';
  font-weight: 300;
  max-width:500px;
}
</style>
