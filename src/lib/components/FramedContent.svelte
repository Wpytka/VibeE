<script lang="ts">
	let title = "";
	let content = "";
	export { title, content };
	export let colored = false;
</script>

<div class="frame" class:colored>
	<h3>{title}</h3>
	<p>{content}</p>
</div>

<style>
	.frame {
		background: #fff;
		border: 1px solid #ddd;
		padding: 1.5rem;
		box-shadow: inset 0 0 5px rgba(0,0,0,0.1);
	}

	.colored {
		border-left: 5px solid #ff4500;
	}

	h3 {
		font-weight: 700;
		margin-bottom: 1rem;
		color: #000;
	}

	p {
		color: #000;
	}
</style>
