<script>
  let tray1out = false;
</script>

<style>
  .container {
    position: relative;
    width: 50%;
    height: 320px;
    border: 1px solid black;
    background-color: rgba(135, 220, 236, 1)
  }

  .contained {
    position: absolute;
    /* left: 0; */
  }

  .box {
    width: 100%;
    height: 145px; 
    border: 1px solid black;
  }

  .bottom-right {
    position: absolute;
    bottom: 0px;
    right: 0px;
    margin: 4px;
  }

  .tray-0 {
    position: absolute;
    top: 0px;
  }
  .tray-1 {
    position: absolute;
    top: 23px;
  }
</style>

<h1>SlidingTray</h1>
<div class='container'>
  <div class='contained box tray-1' style='transition: transform 0.8s;{tray1out ? 'transform: translate(0px, 125px);' : ''} background-color:red; '>
      <input class='contained bottom-right' type="checkbox" bind:checked={tray1out} >
    <div class='contained' style='position: absolute; bottom: 0px;'>Tray 1</div>
  </div>
  <div class='contained box tray-0' style='background-color:green; '>
    <!-- <div class='contained bottom-right'>
      <input type="checkbox" bind:checked={trayXout} style='position:static;'>
    </div> -->
    <div class='contained' style='position: absolute; bottom: 0px;'>Tray 0</div>
  </div>
  <div class='contained' style='position: absolute; bottom: 0px;'>Tray Container</div>
</div>


