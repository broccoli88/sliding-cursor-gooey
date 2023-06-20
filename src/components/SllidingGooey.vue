<script setup>
	import { gsap } from "gsap";
	import { reactive, ref } from "vue";

	const letters = reactive(["A", "B", "C", "D", "E"]);
	const gooey = ref();

	const tl = gsap.timeline();

	const updatePosition = (index) => {
		tl.to(gooey.value, {
			duration: 0.5,
			x: 130 * index,
			scaleX: 1.5,
			ease: "bounce.out",
		}).to(
			gooey.value,
			{
				duration: 0.2,
				scaleX: 1,
			},
			"-=0.2"
		);
	};
</script>

<template>
	<div class="container" @mousemove="checkPosition">
		<header>
			<h1>Sliding <span class="color-word">Gooey</span> Animation</h1>
		</header>

		<ul class="list">
			<li
				@click="updatePosition(index)"
				v-for="(letter, index) in letters"
				:key="index"
				class="list-item"
			>
				{{ letter }}
			</li>

			<div class="gooey" ref="gooey"></div>
		</ul>
	</div>
</template>
<!-- offset left: 228 top: 0  -->
<style lang="scss" scoped>
	.container {
		width: 100vw;
		height: 100vh;
		display: grid;
		place-items: center;
		gap: 3rem;

		background-image: linear-gradient(
			dodgerblue,
			hsl(210, 100%, 76%),
			hotpink
		);
		header {
			align-self: flex-end;
			h1 {
				font-weight: 900;
				color: white;
				.color-word {
					font-weight: 700;

					color: darkblue;
				}
			}

			.pointer-bg {
				color: black;
				font-size: 2rem;
			}
		}

		.list {
			align-self: flex-start;
			list-style: none;
			display: grid;
			grid-auto-flow: column;
			padding-left: 0;
			gap: 5rem;

			position: relative;

			.gooey {
				position: absolute;
				width: 80px;
				aspect-ratio: 1;
				border-radius: 50%;
				background-color: hsl(0, 0%, 100%, 0.5);

				top: -15px;
				left: -15px;
			}

			.list-item {
				width: 50px;
				aspect-ratio: 1;
				border-radius: 50%;
				background-color: darkblue;

				display: flex;
				align-items: center;
				justify-content: center;

				font-weight: 900;
				color: white;
				cursor: pointer;
			}
		}
	}
</style>
