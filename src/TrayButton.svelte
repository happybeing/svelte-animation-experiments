<!-- An animated button for opening and closing a container 'tray'

The idea is for a down arrown (open tray) which animates to become an up 
arrow (close tray) at during the animation of the tray sliding out, and
vice versa.

-->
<script>
export let width = 12;
export let height = 12;

export let pointDown = true;

// export let fill = '#98d02e';
// export let stroke = '#65b81d';
export let fill = '#65b81d';
export let stroke = '#65b81d';
export let strokeWidth = 2;

$: colourStyles = `fill: ${fill}; 
                    stroke: ${stroke}; 
                    stroke-width: ${strokeWidth}; 
                    width: ${width}; 
                    height: ${height};`;

$: triangleStyle = colourStyles + `
                      margin: 1 auto; padding:1;
                      width: ${width+strokeWidth}; 
                      height: ${height};`;

</script>

<style>
</style>

<div style='width: inherit; height: inherit;'>
  <svg style='width: inherit; height: inherit;'>
    <polygon on:click={() => pointDown = !pointDown}
      points='{strokeWidth},{-height/2}, {width+strokeWidth},{-height/2} {(width)/2+strokeWidth},{height/2}' 
      style="{triangleStyle} transform: translate(0px, {height}px); transition: transform 0.8s;{pointDown ? '' : 'transform: translate(0px,' + height + 'px) rotateX(180deg)'}" />
  </svg>
</div>