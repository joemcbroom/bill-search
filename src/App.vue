<template>
	<div id="app">
		<SearchForm />
		<div class="footer">
			<div
				class="hints"
			>hints: "weapon", "missile", "munition", "doctor", "nurse", "corruption"</div>
		</div>
	</div>
</template>

<script>
import SearchForm from "./components/SearchForm";

export default {
	name: "App",
	components: {
		SearchForm,
	},
};
</script>

<style>
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
	height: 100vh;
}
.footer {
	position: absolute;
	bottom: 0;
	width: 100%;
	padding-bottom: 100px;
	display: flex;
	justify-content: center;
}
.hints {
	padding: 15px;
	background-color: cornflowerblue;
}
</style>
