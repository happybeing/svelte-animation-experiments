<script>
import CrossfadeTodoExample from './CrossfadeTodoExample.svelte';
import SlidingTray from './SlidingTray.svelte';
import TrayButton from './TrayButton.svelte';
import Playground from './Playground.svelte';
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
    height: 100%;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

<main>
  <Playground />
  <!-- <TrayButton width={200} height={200}  /> -->
</main>

