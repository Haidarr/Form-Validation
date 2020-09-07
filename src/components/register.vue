<template>
<div class="jumbotron">
    <div class="container">
      <div class="row">
        <div class="col-sm-6 offset-sm-3">
            <h2>Registration Form</h2>
            <h5 class="mb-5">Vue.js ^2.6.x and VeeValidate ^3.3.x</h5>

            <ValidationObserver ref="form">
                <form @submit.prevent="onSubmit" @reset="resetForm">            
                    <div class="form-group">
                        <ValidationProvider name="First Name" rules="required|alpha" v-slot="{ valid, errors }">
                            <input type="text" v-model="first_name" class="form-control" :class="{'border-danger':errors[0], 'border-success':(valid && first_name) }" placeholder="First Name">
                            <span class="text-danger">{{ errors[0] }}</span>
                        </ValidationProvider>
                    </div>
                    <div class="form-group">
                        <ValidationProvider name="Last Name" rules="required|alpha" v-slot="{ valid, errors }">
                            <input v-model="last_name" type="text" class="form-control" :class="{ 'border-danger':errors[0], 'border-success':(valid && first_name) }" placeholder="Last Name">
                            <span class="text-danger">{{ errors[0] }}</span>
                        </ValidationProvider>
                    </div>
                    <div class="form-group">
                        <ValidationProvider name="E-mail" rules="required|email" v-slot="{ valid, errors }">
                            <input v-model="email" type="email" class="form-control" :class="{ 'border-danger':errors[0], 'border-success':(valid && first_name) }" placeholder="E-Mail">
                            <span class="text-danger">{{ errors[0] }}</span>
                        </ValidationProvider>
                    </div>
                    <div class="form-group">
                        <ValidationProvider name="Password" rules="required|confirmed:confirm_password" v-slot="{ valid, errors }">
                            <input type="password" v-model="password" class="form-control" :class="{ 'border-danger':errors[0], 'border-success':(valid && first_name) }" placeholder="Password">
                            <span class="text-danger">{{errors[0]}}</span>
                        </ValidationProvider>
                    </div>
                    <div class="form-group">
                        <ValidationProvider name="Confirm Password" rules="required" v-slot="{ valid, errors }" vid="confirm_password">
                            <input type="password" v-model="confirm_password"  class="form-control" :class="{ 'border-danger':errors[0], 'border-success':(valid && first_name) }" placeholder="Confirm Password">
                            <span class="text-danger">{{errors[0]}}</span>
                        </ValidationProvider>
                    </div>

                    <div class="form-check mb-4">
                      <ValidationProvider name="Agreement" rules="required" v-slot="{ errors }">
                        <input type="checkbox" v-model="agree" class="form-check-input" id="agree">
                        <label class="form-check-label" for="agree">I hereby accept the terms and conditions.</label>
                        <span class="text-danger d-block" v-if="errors[0]">Please accept the Terms and Conditions</span>
                      </ValidationProvider>
                    </div>
       
                    <button type="submit" class="btn btn-primary mr-2">Register</button>
                    <button type="reset" class="btn btn-secondary">Reset</button>
                </form>
            </ValidationObserver>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  data: () => ({
    first_name: '',
    last_name: '',
    email: '',
    password: '',
    confirm_password: '',
    agree: null
  }),
  methods: {
    resetForm(){
      this.first_name = 
      this.last_name = 
      this.email = 
      this.password = 
      this.confirm_password = 
      this.agree = '';
      this.$refs.form.reset();
    },
    onSubmit () {
      this.$refs.form.validate().then(success => {
        if (!success) {
          return;
        }
        alert('You have been successfully registered!');
        // Resetting Values
        this.resetForm();
        // Wait until the models are updated in the UI
        this.$nextTick(() => {
          this.$refs.form.reset();
        });
      });
    }
  }
};
</script>


