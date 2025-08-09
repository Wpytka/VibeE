<script lang="ts">
	import Header from "$lib/components/Header.svelte";
	import Footer from "$lib/components/Footer.svelte";
	import FramedContent from "$lib/components/FramedContent.svelte";
	import HiFiBargraph from "$lib/components/HiFiBargraph.svelte";
	import SideContent from "$lib/components/SideContent.svelte";

	let content = [
        { title: "MODEL NO.", content: "HX-M77" },
        { title: "TAPE TYPE", content: "TYPE IV (METAL)" },
        { title: "DOLBY NR", content: "C" },
        { title: "OUTPUT LEVEL", content: "-3dB" },
        { title: "BIAS", content: "+2" },
        { title: "RECORD LEVEL", content: "+5dB" },
        { title: "CHANNEL", content: "STEREO" },
        { title: "INPUT", content: "LINE" },
        { title: "TIMER", content: "OFF" },
	];
</script>

<Header />

<main>
    <div class="main-content">
        <div class="side-content-wrapper">
            <SideContent />
        </div>
        <div class="bargraph-wrapper">
            <HiFiBargraph />
        </div>
    </div>
    <h2 class="main-title">System Control</h2>
	<div class="grid-container">
		{#each content as item, i}
			<FramedContent title={item.title} content={item.content} colored={i === 0} />
		{/each}
	</div>
</main>

<Footer />

<style>
	main {
		padding: 2rem;
	}

    .main-content {
        display: grid;
        grid-template-columns: 1fr 2fr;
        gap: 2rem;
        width: 100%;
    }

    .main-title {
        color: #fff;
		font-weight: 700;
        text-align: center;
        margin-bottom: 2rem;
        font-size: 2rem;
    }

	.grid-container {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
		gap: 1rem;
	}
</style>
