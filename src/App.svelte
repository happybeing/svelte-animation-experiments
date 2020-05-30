<script>
import Tray from './Tray.svelte';
import TrayHolder from './TrayHolder.svelte';
import TrayButton from './TrayButton.svelte';

import CrossfadeTodoExample from './CrossfadeTodoExample.svelte';
import SlidingTrayTest1 from './SlidingTrayTest1.svelte';
import Playground from './Playground.svelte';
</script>

<style>
	main {
		text-align: left;
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
  <!-- <Playground /> -->
  <!-- <TrayButton width={200} height={200}  /> -->

  <h1>Demo of tray container</h1>
  <p>Uses TrayHolder and Tray components (and the tray uses TrayButton).</p>
  <p>Click the green triangles on the right to open or close the trays.</p>

  <div style='width: inherit; height=inherit;'>
    <TrayHolder>
      <Tray>
        <p>Here's something in the tray</p>
        <p>Here's something in the tray</p>
        <p>Here's something in the tray</p>
        <p>Here's something in the tray</p>
      </Tray>
      <Tray>
        More in this tray. <br/>
        More in this tray. <br/>
        More in this tray. <br/>
        More in this tray. <br/>
      </Tray>
    </TrayHolder>
  </div>
  <p>Some content after the tray.</p>

</main>

