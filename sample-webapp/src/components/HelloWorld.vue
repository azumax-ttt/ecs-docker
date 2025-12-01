<template>
	<div class="hello">
		<h1>This application is Sample WebApp for CICD lesson.</h1>
		<div>Response from REST API is... {{ info }}</div>
		<div v-if="error" class="error">Error: {{ error }}</div>
		<div v-if="loading" class="loading">Loading...</div>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: "HelloWorld",
	props: {
		msg: String,
	},
	data() {
		return {
			info: null,
			error: null,
			loading: true,
		};
	},
	mounted() {
		const BACKEND_URL = "https://braviax.jp/api";
		console.log("Attempting to fetch from:", BACKEND_URL);

		axios
			.get(BACKEND_URL)
			.then((response) => {
				console.log("API response:", response.data);
				this.info = response.data;
				this.loading = false;
			})
			.catch((error) => {
				console.error("API call failed:", error);
				this.error = `${error.message} - 外部APIへの接続に失敗しました`;
				this.info = "Failed to load data";
				this.loading = false;
			});
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
	margin: 40px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
	color: #42b983;
}
.error {
	color: red;
	margin-top: 10px;
	padding: 10px;
	border: 1px solid red;
	border-radius: 4px;
}
.loading {
	color: #42b983;
	margin-top: 10px;
}
</style>
