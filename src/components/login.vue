<template>
	<div class="login screen-padding">
		<figure class="login_logo">
			<img src="../assets/app.png">
			<h1 class="login_title">Vecino</h1>
		</figure>
		<div class="login_form">
			<input type="email" v-model="email" placeholder="Correo" class="input">
			<input type="password" v-model="password" placeholder="Contraseña" class="input">
			<button class="btnAction" v-on:click="loginUser">Ingresar</button>
		</div>
		<router-link to="registro" class="btnSignin">Crear cuenta</router-link>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				email: '',
				password: '',
			}
		},
		mounted() {
			if(firebase.auth().currentUser){
				this.$router.push('in/ordenes')
			}
		},
		methods: {
			loginUser() {
				let data = this;
				firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(function(){
					console.log('todo fue un exito');
					data.$router.push('in/ordenes')
				}).catch(function(error) {
				 console.log('error de datos');
				  // ...
				});
				this.email = '';
				this.password = '';
			}
		}
	}
</script>

<style scoped>
	.login{
		width: 100%;
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-around;
	}
	.login_logo{
		width: 100%;
		max-height: 150px;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.login_logo img{
		width: 100px;
		height: 100px;
	}
	.login_title{
		font-family: 'Lobster', cursive;
		color: #5f5e70;
	}
	.login_form{
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.btnAction{
		margin-top: 30px;
		background-color: #40CC93;
		color: #FFF;
	}
	.btnSignin{
		color: #40CC93;
	}
</style>