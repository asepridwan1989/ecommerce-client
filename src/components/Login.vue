<template >
    <div class="card">
        <h3>Login if you have account !</h3> 
        <p style="color:red">{{error}}</p>
        <div class="card-body">
            <form>                
                <div class="form-group">
                    <label for="exampleInputEmail1">Email address</label>
                    <input type="text" class="form-control" aria-describedby="emailHelp" placeholder="Enter email" v-model="email">
                </div>
                <div class="form-group">
                    <label for="exampleInputPassword1">Password</label>
                    <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password" v-model="password">
                </div>
                <div class="form-check">
                </div>
                <button type="submit" class="btn btn-primary" @click="login">Login</button>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Login',
        data(){
            return{
                email:"",
                password:"",
                token:"",
                fail:false,
                error:"",
                user:""
            }
        },
        methods: {
            login() {
                let payload = {
                    email: this.email,
                    password: this.password
                }
                let objUser = {}
                // console.log(payload)
                let self = this
                 axios.post('https://arcane-falls-85350.herokuapp.com/users/signin', payload)
                  .then( response => {
                      console.log(response.data.dataUser.email)
                      self.token = response.data.token
                      self.user = response.data.dataUser
                      console.log('self user', self.user)
                    //   alert("succesfuly registered")
                      // success = true
                      objUser.email = self.user.email
                      objUser.role = self.user.role
                      window.location.reload(true);
                      localStorage.setItem('commerce-token', self.token);
                      localStorage.setItem('com-user', self.user.email);
                      localStorage.setItem('com-role', self.user.role);
                  })
                  .catch( err => {
                        this.error = err.response.data.message
                        console.log('errrorrrr',err)
                  })
            }
        } 
    }
</script>

