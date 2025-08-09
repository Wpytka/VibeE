<script lang="ts">
	import { onMount } from 'svelte';
    import { goto } from '$app/navigation';

	let container: HTMLDivElement;
	let bars: HTMLDivElement[] = [];

	onMount(() => {
		const handleMouseMove = (e: MouseEvent) => {
			const rect = container.getBoundingClientRect();
			const mouseX = e.clientX - rect.left;

			bars.forEach((bar, i) => {
                if(!bar) return;
				const barX = bar.offsetLeft + bar.offsetWidth / 2;
				const distance = Math.abs(mouseX - barX);
				const maxDistance = rect.width / 2;
				const heightPercentage = Math.max(0, 100 - (distance / maxDistance) * 100);
				bar.style.transform = `scaleY(${heightPercentage / 100})`;
			});
		};

		container.addEventListener('mousemove', handleMouseMove);

		return () => {
			container.removeEventListener('mousemove', handleMouseMove);
		};
	});

    function navigateTo(path: string) {
        goto(path);
    }
</script>

<div class="graph-wrapper">
    <div class="bargraph-container" bind:this={container}>
        <a href="/delivery" on:click|preventDefault={() => navigateTo('/delivery')} class="graph-column">
            <div class="bars-container">
                {#each Array(10) as _, i}
                    <div class="bar-wrapper">
                        <div class="bar" bind:this={bars[i]}>
                            {#each Array(10) as _}
                                <div class="square-block">
                                    {#each Array(6) as _}
                                        <div class="square"></div>
                                    {/each}
                                </div>
                            {/each}
                        </div>
                        <span class="bar-number">{i + 1}</span>
                    </div>
                {/each}
            </div>
        </a>
        <div class="separator"></div>
        <a href="/support" on:click|preventDefault={() => navigateTo('/support')} class="graph-column">
            <div class="bars-container">
                {#each Array(10) as _, i}
                    <div class="bar-wrapper">
                        <div class="bar" bind:this={bars[i + 10]}>
                            {#each Array(10) as _}
                                <div class="square-block">
                                    {#each Array(6) as _}
                                        <div class="square"></div>
                                    {/each}
                                </div>
                            {/each}
                        </div>
                        <span class="bar-number">{i + 11}</span>
                    </div>
                {/each}
            </div>
        </a>
        <div class="separator"></div>
        <a href="/rescue" on:click|preventDefault={() => navigateTo('/rescue')} class="graph-column">
            <div class="bars-container">
                {#each Array(10) as _, i}
                    <div class="bar-wrapper">
                        <div class="bar" bind:this={bars[i + 20]}>
                            {#each Array(10) as _}
                                <div class="square-block">
                                    {#each Array(6) as _}
                                        <div class="square"></div>
                                    {/each}
                                </div>
                            {/each}
                        </div>
                        <span class="bar-number">{i + 21}</span>
                    </div>
                {/each}
            </div>
        </a>
    </div>
    <div class="labels-container">
        <div class="label-column"><span>delivery</span></div>
        <div class="separator"></div>
        <div class="label-column"><span>support</span></div>
        <div class="separator"></div>
        <div class="label-column"><span>rescue</span></div>
    </div>
</div>

<style>
    .graph-wrapper {
        position: relative;
        padding: 1rem 1rem 0rem 1rem;
        background-color: black;
        border-left: 1px dashed #f0f8ff;
        border-right: 1px dashed #f0f8ff;
        overflow: hidden;
        height: 100%;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
    }

    .graph-wrapper::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-image: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><filter id="noise"><feTurbulence type="fractalNoise" baseFrequency="0.65" numOctaves="3" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(%23noise)"/></svg>');
        opacity: 0.1;
        pointer-events: none;
    }

	.bargraph-container {
		display: flex;
		justify-content: space-between;
		align-items: flex-end;
		flex-grow: 1;
	}

    .graph-column {
        display: flex;
        justify-content: center; /* Changed to center for better alignment */
        align-items: flex-end;
        height: 100%;
        text-decoration: none;
        flex-grow: 1;
        flex-basis: 33.33%;
        overflow: hidden;
    }

    .bars-container {
        display: flex;
        justify-content: center;
        align-items: flex-end;
        height: 100%;
        width: 100%;
    }

    .separator {
        width: 1px;
        height: 100%;
        background-image: repeating-conic-gradient(#f0f8ff 0% 25%, transparent 0% 50%);
        background-size: 4px 4px;
        box-shadow: 0 0 3px rgba(255, 255, 255, 0.5);
    }

    .bar-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        height: 100%;
        flex-grow: 1;
        flex-basis: 0;
        padding: 0 2px;
    }

	.bar {
	width: 100%;
        height: 100%; /* Set to full height */
	transform: scaleY(0); /* Initially scaled to 0 */
	transform-origin: bottom;
	transition: transform 0.1s ease-out; /* Animate transform */
        display: flex;
        flex-direction: column-reverse;
        overflow: hidden;
	    filter: drop-shadow(0 0 3px rgba(255, 255, 255, 0.7));
	}

    .square-block {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start; /* Align items to the start to control spacing with gap */
        gap: 1px; /* all gap between squares */
        margin-bottom: 2px;
        flex-shrink: 0;
    }

    .square {
        width: calc((100% - 4px) / 3); /* Adjust width to account for 2px gaps between 3 squares */
        aspect-ratio: 1;
        background-color: #f0f8ff;
    }

    .bar-number {
        margin-top: 0.5rem;
        font-size: 0.75rem;
        color: #888;
        text-shadow: 0 0 2px rgba(255, 255, 255, 0.5);
    }

    .labels-container {
        display: flex;
        justify-content: space-between; /* Changed to space-between for alignment */
        padding-top: 1rem;
        margin-top: 0rem;
        align-items: center;
    }

    .labels-container .separator {
        height: 2rem; /* Set a fixed height for visibility */
    }

    .label-column {
        flex-grow: 1;
        flex-basis: 33.33%; /* Ensure equal distribution for 3 columns */
        text-align: center;
    }

    .labels-container span {
        color: #ccc;
        font-weight: 700;
        text-transform: uppercase;
        text-shadow: 0 0 2px rgba(255, 255, 255, 0.5);
    }
</style>
