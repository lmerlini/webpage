<template>
	<div class="container">
		<div class="card">
			<div class="row">
				<h1 class="title__result">Your Result</h1>

				<div class="circle">
					<h1 class="score">{{ score }}</h1>
					<span class="score__to">of 100</span>
				</div>

				<div class="congrats" v-if="score">
					<h1 class="great">
						{{ resultCongrants }}
					</h1>
					<p class="text-congrats">
						{{ resultFormat }}
					</p>
				</div>
			</div>
			<div class="summary">
				<h1 class="title__sumary">Summary</h1>
				<card-content
					v-for="(data, index) in dataJson"
					:key="index"
					:icon="`${data.icon}`"
					:title="data.category"
					:score="data.score"
					@update:score="updateScore"
				>
				</card-content>

				<button>Continue</button>
			</div>
		</div>
	</div>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";
import CardContent from "./CardContent.vue";
onMounted(() => {
	fetch("./data.json")
		.then((res) => res.json())
		.then((result) => {
			dataJson.value = result;
		})
		.catch((error) =>
			console.log(`Houve um erro na importação. ::. ${error} .::`)
		);
});

const score = ref(0);
const dataJson = ref(null);

function updateScore(data) {
	score.value = data.score;
}
const resultFormat = computed(() => {
	return score.value > 60
		? "You scored higher than 65% of the people who have taken these tests."
		: "Sorry you can do it again!!!";
});

const resultCongrants = computed(() => {
	return score.value > 60 ? "Great" : "Ooops";
});

components: {
	CardContent;
}
</script>

<style scoped>
.title__result {
	color: #ffffff93;
	font-size: 1.5rem;
	font-weight: 500;
}
.summary {
	width: 50%;
	padding: 1.875rem;
}
.title__sumary {
	font-family: "HankenGroteskExtraBold";
	letter-spacing: 1px;
	font-weight: 500;
	font-size: 1.3rem;
	margin-bottom: 0.94rem;
}
.container {
	display: flex;
	justify-content: center;
	align-items: center;
	width: 100%;
	height: 100vh;
}
.card {
	display: flex;
	width: 42rem;
	height: 28.75rem;
	background: #fff;
	box-shadow: 0 0 20rem 1rem #9c9b9b98;
	border-radius: 1.25rem;
}

.row {
	background: linear-gradient(to bottom, #4a23cc, #4734ef);
	border-radius: 1.25rem;
	width: 50%;
	height: 100%;
	display: flex;
	justify-content: space-evenly;
	align-items: center;
	flex-direction: column;
}
.circle {
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	width: 11.25rem;
	height: 11.25rem;
	border-radius: 100%;

	background: linear-gradient(to bottom, #451ed1 10%, #4533eb 85%);
}

.score {
	font-size: 4rem;
	color: #fff;
}
.score__to {
	color: #ffffff8f;
}
.great {
	text-align: center;
	color: #fff;
}
.text-congrats {
	padding: 1.25rem 3.125rem;
	text-align: center;
	color: #ffffff8f;
}

@media only screen and (max-width: 720px) {
	.container {
		flex-wrap: wrap;
	}
	.card {
		width: 85%;
		height: max-content;
		flex-direction: column;
		flex-wrap: wrap;
	}
	.title__result {
		font-size: 1.6rem;
	}
	.title__sumary {
		margin: 0;
		text-align: center;
		letter-spacing: 0;
		margin-bottom: 0.94rem;
	}
	.circle {
		width: 5.25rem;
		height: 5.25rem;
		border-radius: 100%;

		background: linear-gradient(to top, #451ed1, #4533eb, blue);
	}
	.great {
		font-size: 1.4rem;
	}
	.text-congrats {
		padding: 0.25rem 1rem 1rem;
		text-align: center;
		color: #ffffff8f;
	}
	.score {
		font-size: 2rem;
		color: #fff;
	}
	.row,
	.summary {
		width: 100%;
	}
	.summary {
		padding: 0.75rem;
	}
}
</style>
