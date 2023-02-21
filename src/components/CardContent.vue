<script setup>
const props = defineProps({
	title: String,
	icon: String,
	score: Number,
});
const emites = defineEmits(["update:score"]);

function active(value) {
	emites("update:score", value);
}
</script>
<template>
	<div
		class="reactangle memory"
		:class="title.toLowerCase()"
		@click="active(props)"
	>
		<div class="img">
			<slot name="icon">
				<img :src="props.icon" alt="" />
			</slot>
			<slot name="title">
				<span> {{ props.title }}</span>
			</slot>
		</div>
		<div>
			<slot name="">
				<span class="emphasi"> {{ props.score }} </span>
				<span class="range">/ 100</span>
			</slot>
		</div>
	</div>
</template>

<style scoped>
.emphasi {
	color: #000000b6;
}
.reactangle {
	margin-top: 0.625rem;
	padding: 0 0.625rem;
	width: 100%;
	height: 3.75rem;
	border-radius: 0.75rem;
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.range {
	color: #00000062;
}

.memory {
	background-color: rgba(255, 189, 34, 0.2);
	color: hsla(42, 100%, 50%, 2);
}
.reaction {
	background-color: rgba(255, 81, 62, 0.2);
	color: hsla(6, 100%, 50%, 2);
}

.verbal {
	background-color: rgba(82, 175, 152, 0.2);
	color: hsla(165, 37%, 50%, 2);
}

.visual {
	background-color: rgba(72, 79, 170, 0.2);
	color: hsla(236, 40%, 50%, 2);
}
.memory:hover {
	transition: background linear 0.4s;
	background-color: rgba(255, 189, 34, 0.5);
	color: hsla(42, 100%, 50%, 5);
}
.reaction:hover {
	transition: background linear 0.4s;
	background-color: rgba(255, 81, 62, 0.5);
	color: hsla(6, 100%, 50%, 5);
}

.verbal:hover {
	transition: background linear 0.4s;
	background-color: rgba(82, 175, 152, 0.5);
	color: hsla(165, 37%, 50%, 5);
}

.visual:hover {
	transition: background linear 0.4s;
	background-color: rgba(72, 79, 170, 0.5);
	color: hsla(236, 40%, 50%, 5);
}
</style>
