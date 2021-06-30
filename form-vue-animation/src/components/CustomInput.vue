 <template id="custom-input">

  <div class="form-group">
    <label class="form-control-label">{{label}}</label>
      <input v-bind="$attrs" 
             :type="type" 
             :value="value" 
             @blur="Validation($event.target.value)"
             :class="{'form-control':true, 'is-invalid': errors}" 
             @input="$emit('update', $event.target.value)"/>   
  <Fade>
    <div v-if="!value" class="invalid-feedback">Please enter something.</div>
    <div v-else class="invalid-feedback">{{inputError}}</div> 
  </Fade>
  </div>

</template>

<script>
import Fade from './../components/Animations/Fade.vue'

export default {
  name: 'CustomInput',
  inheritAttrs: false,
  components: {
    Fade
  },
    data() {
      return {
        errors: false,
        valid: false,
        inputError: ""
      };
    },
    props: {
      label: {
        type: String,
        default: ''
      },
      value: {
        type: [String, Number],
        default: ''
      },
      type: {
        type: String,
        default: '',
      }
      
    },

    model: {
        prop: "value",
        event: "update"
      },
    methods: {
        validName: function(name) {
          var re = /^[a-zA-Z]{6,13}$/;
          return re.test(name);
        },
        isNumeric: function (n) {
          return !isNaN(parseFloat(n)) && isFinite(n);
        },
        validEmail : function(email) {
          var re = /(.+)@(.+){2,}\.(.+){2,}/;
          return re.test(email);
        },
        validPassword: function(p) {
          var re = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{6,13}$/;
          return re.test(p);
        },

        Validation(value){
    
          if( this.label === "Name" ){
              if( this.validName(value)){
              this.errors = false;
              this.valid = true;
              } else {
                this.errors = true;
                this.inputError = "Name must be between 6 and 13 letters"
                this.valid = false;
              }
          }

          if( this.label === "Mobile" ){
              if( this.isNumeric(value)){
                this.errors = false;
                this.valid = true;
                  }else {
                    this.errors = true;
                    this.inputError = "Mobile number must be between 5 and 9 numbers"
                    this.valid = false;
                  }
          }

          if( this.label === "Postcode" ){
              if( this.isNumeric(value)){
                    this.errors = false;
                    this.valid = true;
                  }else {
                    this.errors = true;
                    this.inputError = "Postcode must be between 5 and 9 numbers"
                    this.valid = false;
                  }
          }

          if( this.label === "Email" ){
              if( this.validEmail(value)){
                this.errors = false;
                this.valid = true;
                  }else {
                    this.errors = true;
                    this.inputError = "Please introduce a valid email"
                    this.valid = false;
                  }
          }

          if( this.label === "Password" ){
            if( this.validPassword(value)){
              this.errors = false;
              this.valid = true;
                } else {
                  this.errors = true;
                  this.inputError = "Password must contain one cap, number and special character"
                  this.valid = false;
                } 
        }

          //  if( this.label === "Confirmation" ){
          //     if (this.password.value === this.confirmation.value )
          //     console.log('true')
          //     this.errors = false;
          //     this.valid = true;
          //   } else {
          //     this.errors = true;
          //     this.inputError = "Passwords don't match"
          //     this.valid = false;
          //     }

          this.$emit('getvalidation', this.valid, this.label)
    },
    }
}
</script>
