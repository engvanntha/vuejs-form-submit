<script>
export default {
	data() {
		return {
			email: '',
			password: '',
			role: 'developer',
			terms: false,
			tempSkill: '',
			skills: [],
			passwordErrors: ''
		}
	},
	methods: {
		addSkill(e) {
			if (e.key === ',' && this.tempSkill) {
				if (!this.skills.includes(this.tempSkill)) {
					this.skills.push(this.tempSkill)
				}
				this.tempSkill = ''
			}
		},
		deleteSkill(skill) {
			this.skills = this.skills.filter((item) => {
				return skill !== item
			})
		},
		handleSubmit() {
			this.passwordErrors = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
			if (!this.passwordErrors) {
				console.log('email', this.email)
				console.log('password', this.password)
				console.log('role', this.role)
				console.log('term', this.terms)
				console.log('skills', this.skills)
			}
		}
	}
}
</script>

<template>
	<form action="" @submit.prevent="handleSubmit">
		<label for="">Email:</label>
		<input type="email" required v-model="email">
		<label for="">Password:</label>
		<input type="password" required v-model="password">
		<div v-if="passwordErrors" class="error"> {{passwordErrors}}</div>
		<label for="">Role:</label>
		<select name="" id="" v-model="role">
			<option value="">-- Select your role</option>
			<option value="developer">Web Developer</option>
			<option value="designer">Web Designer</option>
		</select>

		<label for="">Skills</label>
		<input type="text" v-model="tempSkill" @keyup.alt="addSkill">
		<div v-for="skill in skills" :key="skill" class="pill skill-text">
			<p @click="deleteSkill(skill)">{{ skill }}</p>
		</div>
		<div class="terms">
			<input type="checkbox" required v-model="terms">
			<label for="">Accept terms and conditions</label>
		</div>
		<div class="submit">
			<button>Create an Account</button>
		</div>
	</form>
	<div>
		<p>Email: {{ email }}</p>
		<p>Password: {{ password }}</p>
		<p>Role: {{ role }}</p>
		<p>Term: {{ terms }}</p>
	</div>
</template>

<style>
form {
	width: 420px;
	margin: 30px auto;
	background: white;
	text-align: left;
	padding: 40px;
	border-radius: 10px;
}

label {
	color: #aaa;
	display: inline-block;
	margin: 25px 0 15px;
	font-size: 0.6rem;
	text-transform: uppercase;
	letter-spacing: 1px;
	font-weight: bold;
}

p {
	color: #181818;
}

input, select {
	display: block;
	padding: 10px 6px;
	width: 100%;
	box-sizing: border-box;
	border: none;
	border-bottom: 1px solid #ddd;
	color: #555;
}

input[type="checkbox"] {
	display: inline-block;
	width: 16px;
	margin: 0 10px 0 0;
	position: relative;
	top: 2px;
}

.skill-text {
	color: #222222;
}

.pill {
	display: inline-block;
	margin: 20px 10px 0 0;
	padding: 6px 12px;
	background: #eee;
	border-radius: 20px;
	font-size: 12px;
	letter-spacing: 1px;
	font-weight: bold;
	color: #777;
	cursor: pointer;
}

button {
	background: #0b6dff;
	border: 0;
	padding: 10px 20px;
	margin-top: 20px;
	color: white;
	border-radius: 20px;
}

.submit {
	text-align: center;
}
.error {
	color: #ff0062;
	margin-top: 10px;
	font-size: 0.8rem;
	font-weight: bold;
}
</style>