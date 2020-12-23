<template>
	<div class="search-form">
		<div
			class="loading-spinner"
			v-show="loading"
		>
			<div class="sk-chase">
				<div class="sk-chase-dot"></div>
				<div class="sk-chase-dot"></div>
				<div class="sk-chase-dot"></div>
				<div class="sk-chase-dot"></div>
				<div class="sk-chase-dot"></div>
				<div class="sk-chase-dot"></div>
			</div>
		</div>
		<div v-show="!loading">
			<h3>Search HR133 (Covid "Relief" Package) for a term</h3>
			<a
				class="bill-link"
				href="https://rules.house.gov/sites/democrats.rules.house.gov/files/BILLS-116HR133SA-RCP-116-68.pdf"
				target="_blank"
			>Bill Text (pdf)</a>
			<form ref="form">
				<input
					v-model="input"
					placeholder="Enter Search Term"
				/>
				<button @click.prevent="submit()">Submit</button>
			</form>

			<ul
				v-for="item in results"
				:key="item.term"
			>
				<li>
					The word
					<span class="search-term">{{ item.term }}</span>
					occurs
					<span class="occurences">{{ item.occurences }}</span>
					times
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	name: "HelloWorld",
	data() {
		return {
			input: "",
			billText: [],
			submitted: false,
			results: [],
			loading: true,
		};
	},
	methods: {
		submit: function () {
			const term = this.input;
			const occurences = this.billText.reduce((acc, curr) => {
				return (acc += curr
					.toLowerCase()
					.includes(term.toLowerCase().trim()));
			}, 0);
			this.results.push({
				term: term,
				occurences: occurences,
			});
		},
	},
	created() {
		let text = require("../assets/bill_text.txt").default;
		this.billText = text.split("\n");
		this.loading = false;
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
	text-decoration: none;
	color: cornflowerblue;
}
a:hover {
	text-decoration: underline;
}
h3 {
	margin-bottom: 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
input {
	margin-top: 10px;
}

.search-term,
.occurences {
	font-weight: bold;
	font-size: 1.2rem;
}
.search-term {
	/* text-decoration: underline; */
	border: 1px solid black;
	padding: 0 5px;
}
.occurences {
	color: cornflowerblue;
	padding-left: 5px;
}
.loading-spinner {
	display: flex;
	justify-content: center;
}
.sk-chase {
	width: 40px;
	height: 40px;
	position: relative;
	animation: sk-chase 2.5s infinite linear both;
}

.sk-chase-dot {
	width: 100%;
	height: 100%;
	position: absolute;
	left: 0;
	top: 0;
	animation: sk-chase-dot 2s infinite ease-in-out both;
}

.sk-chase-dot:before {
	content: "";
	display: block;
	width: 25%;
	height: 25%;
	background-color: cornflowerblue;
	border-radius: 100%;
	animation: sk-chase-dot-before 2s infinite ease-in-out both;
}

.sk-chase-dot:nth-child(1) {
	animation-delay: -1.1s;
}
.sk-chase-dot:nth-child(2) {
	animation-delay: -1s;
}
.sk-chase-dot:nth-child(3) {
	animation-delay: -0.9s;
}
.sk-chase-dot:nth-child(4) {
	animation-delay: -0.8s;
}
.sk-chase-dot:nth-child(5) {
	animation-delay: -0.7s;
}
.sk-chase-dot:nth-child(6) {
	animation-delay: -0.6s;
}
.sk-chase-dot:nth-child(1):before {
	animation-delay: -1.1s;
}
.sk-chase-dot:nth-child(2):before {
	animation-delay: -1s;
}
.sk-chase-dot:nth-child(3):before {
	animation-delay: -0.9s;
}
.sk-chase-dot:nth-child(4):before {
	animation-delay: -0.8s;
}
.sk-chase-dot:nth-child(5):before {
	animation-delay: -0.7s;
}
.sk-chase-dot:nth-child(6):before {
	animation-delay: -0.6s;
}

@keyframes sk-chase {
	100% {
		transform: rotate(360deg);
	}
}

@keyframes sk-chase-dot {
	80%,
	100% {
		transform: rotate(360deg);
	}
}

@keyframes sk-chase-dot-before {
	50% {
		transform: scale(0.4);
	}
	100%,
	0% {
		transform: scale(1);
	}
}
</style>
