<template>
    <div id="input-form" class="container">
        <div class="row">
            <div class="col-md-10 offset-1">
                <br>
                <h2 id="register-name" class="register-name-card">Register New User</h2>
                <div id="flash-message" >
                    <span v-if="server_response !=''" class="alert flash-message" role="alert"
                          :class="{'alert-success': registered, 'alert-warning': !registered}" >{{ server_response}}</span>
                </div>

                <form class="text-sm-left register-form" @submit.prevent="register" enctype="multipart/form-data">
                    <div class="row">
                        <div class="col-md-6 form-group">
                            <label for="new_username" >Username *</label>
                            <input type="text" id="new_username" class="form-control" v-model="newUser.username" required>
                        </div>
                        <div class="col-md-6 form-group">
                            <label for="new_password" >Password *</label>
                            <input type="password" id="new_password" class="form-control" v-model="newUser.password"required>
                        </div>
                    </div>

                    <div class="row">
                        <div class="col-md-4 form-group">
                            <label for="firstname" >First Name</label>
                            <input type="text" id="firstname" class="form-control" v-model="newUser.firstname">
                        </div>

                        <div class="col-md-4 form-group">
                            <label for="middlename" >Middle Name</label>
                            <input type="text" id="middlename" class="form-control" v-model="newUser.middlename">
                        </div>

                        <div class="col-md-4 form-group">
                            <label for="lastname" >Last Name</label>
                            <input type="text" id="lastname" class="form-control" v-model="newUser.lastname">
                        </div>
                    </div>

                    <div class="row">
                        <div class="col-md-4 form-group">
                            <label for="email" >Email</label>
                            <input type="email" id="email" class="form-control" v-model="newUser.email">

                        </div>

                        <div class="col-md-4 form-group">
                            <label for="phone" >Phone</label>
                            <input type="text" id="phone" class="form-control" v-model="newUser.phone">
                        </div>

                        <div class="col-md-4 form-group">
                            <label for="gender">Gender</label>
                            <select name="gender" id="gender" class="form-control" v-model="newUser.gender">
                                <option value="M">Male</option>
                                <option value="F">Female</option>
                            </select>
                        </div>
                    </div>

                    <div class="row">
                        <div class="col-md-12 text-center">
                            <button class="btn btn-sm btn-warning uniform-width" type="submit">Register</button>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
	export default {
		name: 'add-user',
		data(){
			return{
				newUser: {
					username: '',
					password: '',
					email: '',
					firstname: '',
					middlename: '',
					lastname:'',
					phone:'',
					gender: '',
					type:'viewer'
				},
				server_response: '',
				registered: false
			}
		},
		methods: {
			register: function(){
				//console.log("Register new user")
				let uri = this.$hostname + 'register'
				this.axios.post(uri, this.newUser).then( (response) => {
					console.log(response)
					if (response.data.registered){
						this.registered = true
						this.server_response = `User '${this.newUser.username}' is Successfully Registered`
					}else{
						this.registered = false
						this.server_response = `User '${this.newUser.username}' was not Registered`
					}
				})
			},
		}
	}
</script>

<style scoped>
    .hidden{
        display: none;}
    .not-hidden{
        display: block;}
</style>

