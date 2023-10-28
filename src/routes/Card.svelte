<!-- SVGViewer.svelte -->

<script lang="ts">
  export let color: 'R' | 'G' | 'B'
  export let pattern: 'C' | 'S' | 'D'
  export let filled: 'N' | 'B' | 'F'
  export let number: '1' | '2' | '3'
  export let selected: boolean = false
  $: c = color === 'R' ? "#ff0099" : color === 'G' ? "#009900" : "#3333ff"
</script>

<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="0 0 40 58" role="button" on:keypress on:click>
  <defs>
    <pattern id="R" patternUnits="userSpaceOnUse" width="2" height="2">
      <circle cx="0" cy="0" r="9" fill-opacity="0" />
      <path d="M 1,0 V 2" stroke-width="0.5" stroke={"#ff0099"} />
    </pattern>
    <pattern id="G" patternUnits="userSpaceOnUse" width="2" height="2">
      <circle cx="0" cy="0" r="9" fill-opacity="0" />
      <path d="M 1,0 V 2" stroke-width="0.5" stroke={"#009900"} />
    </pattern>
    <pattern id="B" patternUnits="userSpaceOnUse" width="2" height="2">
      <circle cx="0" cy="0" r="9" fill-opacity="0" />
      <path d="M 1,0 V 2" stroke-width="0.5" stroke={"#3333ff"} />
    </pattern>
  </defs>
  <rect width="40" height="58" rx="3" ry="3" stroke-width="0.3" stroke="#000" fill={selected ? "#ffff99" : "#fff"} />
  <g transform="translate(20,29)" fill={filled === 'N' ? "#fff" : filled === 'B' ? `url(#${color})` : `${c}`} fill-opacity={filled === 'N' ? 0 : 1} stroke={c} >
    {#if pattern === 'C'}
      {#if number === "1"}
        <rect id="c1" x="-9" y="-5" width="18" height="10" rx="6" ry="5" transform="translate(0, 0)"/>
      {:else if number === "2"}
        <rect id="c1" x="-9" y="-5" width="18" height="10" rx="6" ry="5" transform="translate(0, -8)"/>
        <rect id="c1" x="-9" y="-5" width="18" height="10" rx="6" ry="5" transform="translate(0, 8)"/>
      {:else}
        <rect id="c1" x="-9" y="-5" width="18" height="10" rx="6" ry="5" transform="translate(0, -12)"/>
        <rect id="c1" x="-9" y="-5" width="18" height="10" rx="6" ry="5" transform="translate(0, 0)"/>
        <rect id="c1" x="-9" y="-5" width="18" height="10" rx="6" ry="5" transform="translate(0, 12)"/>
      {/if}
    {:else if pattern === 'S'}
      {#if number === "1"}
        <path id="b1" d="M -9,0 C -8,-8 0,-3 4,-3 S 9,-8 9,0 C 8,8 0,3 -4,3 S -9,8 -9,0" transform="translate(0, 0)"/>
      {:else if number === "2"}
        <path id="b1" d="M -9,0 C -8,-8 0,-3 4,-3 S 9,-8 9,0 C 8,8 0,3 -4,3 S -9,8 -9,0" transform="translate(0, -8)"/>
        <path id="b1" d="M -9,0 C -8,-8 0,-3 4,-3 S 9,-8 9,0 C 8,8 0,3 -4,3 S -9,8 -9,0" transform="translate(0, 8)"/>
      {:else}
        <path id="b1" d="M -9,0 C -8,-8 0,-3 4,-3 S 9,-8 9,0 C 8,8 0,3 -4,3 S -9,8 -9,0" transform="translate(0, -12)"/>
        <path id="b1" d="M -9,0 C -8,-8 0,-3 4,-3 S 9,-8 9,0 C 8,8 0,3 -4,3 S -9,8 -9,0" transform="translate(0, 0)"/>
        <path id="b1" d="M -9,0 C -8,-8 0,-3 4,-3 S 9,-8 9,0 C 8,8 0,3 -4,3 S -9,8 -9,0" transform="translate(0, 12)"/>
      {/if}
    {:else}
      {#if number === "1"}
        <path d="M -10,0 L 0,-5 L 10,0 L 0,5 Z" transform="translate(0, 0)"/>
      {:else if number === "2"}
        <path d="M -10,0 L 0,-5 L 10,0 L 0,5 Z" transform="translate(0, -8)"/>
        <path d="M -10,0 L 0,-5 L 10,0 L 0,5 Z" transform="translate(0, 8)"/>
      {:else}
        <path d="M -10,0 L 0,-5 L 10,0 L 0,5 Z" transform="translate(0, -12)"/>
        <path d="M -10,0 L 0,-5 L 10,0 L 0,5 Z" transform="translate(0, 0)"/>
        <path d="M -10,0 L 0,-5 L 10,0 L 0,5 Z" transform="translate(0, 12)"/>
      {/if}
    {/if}
  </g>
</svg>
