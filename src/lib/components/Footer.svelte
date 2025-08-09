<script lang="ts">
	let contacts = [
		{
			name: "John Doe",
			email: "john.doe@example.com"
		},
		{
			name: "Jane Doe",
			email: "jane.doe@example.com"
		}
	];
</script>

<footer>
	<h2>Contact Us</h2>
	<ul>
		{#each contacts as contact}
			<li>{contact.name} - {contact.email}</li>
		{/each}
	</ul>
</footer>

<style>
	footer {
		background: #fff;
		padding: 1rem;
		text-align: right;
		border-top: 1px solid #ddd;
		box-shadow: 0 -2px 3px rgba(0,0,0,0.1);
	}

	h2 {
		color: #000;
		font-weight: 700;
	}

	ul {
		list-style: none;
		padding: 0;
	}

	li {
		color: #000;
	}
</style>
