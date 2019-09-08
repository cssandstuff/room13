<script>
	import { onMount } from 'svelte';

	let characters = [
		'Maja', 'Payton', 'Miss Quach',
		'Reef', 'Rylee', 'Noa',
		'Sophie', 'Aayah', 'Olive',
		'Abbie', 'Lucy', 'Cruz',
		'Benson', 'Zion', 'Ariyah',
		'Milly', 'Shekinah', 'Onyx',
		'Nathan', 'Johnny', 'John',
		'Frank', 'Ethan', 'Heath',
		'Kobey', 'Reilloch', 'Zachary',
		'Jaxon',
		];

	let emoji = [
		'🥳', '🎉', '✨',
		'🐠', '🤪', '❤️',
		'🥺', '😻', '😜',
		'😎', '😘', '🙄',
		'🤩', '👍', '🤟',
		'👌', '🙌', '👏',
		'😋', '🐶', '🐹',
		'🦁', '🐭', '🤓',
		'🌸', '🏅', '🏆',
		'⭐️',
		];


	let confetti = new Array(40).fill()
		.map((_, i) => {
			return {
				character: emoji[i % emoji.length] + characters[i % characters.length],
				x: (Math.random() * 50) + 15,
				y: -20 - Math.random() * 300,
				z: i++ * 14,
				r: 0.2 + Math.random() * 0.5,
				s: (Math.random() * 0.55) + 0.3,
			};
		})
		.sort((a, b) => a.r - b.r);

	onMount(() => {
		let frame;

		function loop() {
			frame = requestAnimationFrame(loop);

			confetti = confetti.map(emoji => {
				emoji.y += 0.7 * emoji.r;
				if (emoji.y > 130) emoji.y = -130;
				return emoji;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

<style>
	:global(body, html) {
		width: 100vw;
		height: 100vh;
		overflow: hidden;
		background: rgb(146, 91, 128);
	}
	:global(body) {
		font-family: 'Caveat', cursive;
	}

	span {
		position: absolute;
		font-size: 5vw;
		padding: 0.4em;
		background: #111;
		color: #fff;
		border-radius: 10px;
		font-weight: 300;
		top: -90px;
		display: block;
	}
	.threeD{
		perspective: 900px
	}
	h1{
		display: flex;
		align-items: center;
		background: #fff;
		color: #000;
		font-weight: 500;
		padding: 1em;
		z-index: 999;
		left: 50%;
		margin-left: -150px;
		text-align: center;
		top: 0;
		margin-top: -15px;
		position: absolute;
		border-radius: 5px;
		transform: translateZ(150px);
	}
</style>

<div class="threeD">
<h1>Thank You Room 13!</h1>
{#each confetti as c}
	<span style="transform: translateX({c.x}vw) translateY({c.y}vh) translateZ({c.z}px) rotateZ({c.y/300 * 90}deg) rotateX({c.y/100 * 90}deg) scale({c.s}); opacity:{c.y / 20}">{c.character}</span>
{/each}
</div>