<template>
  <div>
		<h1>Login</h1>
		<form @submit.prevent="login">
			<input v-model="username" placeholder="username">
			<br />
			<br />
			<input v-model="password" placeholder="password" type="password">
			<br />
			<br />
			<button type="submit">Enviar</button>
		</form>
	</div>
</template>

<script>
import { mapMutations } from "vuex";

export default {
	data() {
		return {
			username: '',
			password: '',
		}
	},
	methods: {
		...mapMutations(["setUser", "setToken"]),
		async login(e) {
			e.preventDefault();

			const options = {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},
				body: JSON.stringify({
					username: this.username,
					password: this.password
				})
			};
			const response = await fetch('http://localhost:3000/login', options);
			const { user, token } = await response.json();

			this.setUser(user);
			this.setToken(token);
			this.$router.push('/');
		},
	},
}
</script>