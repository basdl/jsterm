<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { isPrintableCharacter } from "./helper";

  const dispatch = createEventDispatcher();

  export let decimalValue = 0;

  $: asciiValue = isPrintableCharacter(decimalValue)
    ? String.fromCharCode(decimalValue)
    : "?";
  $: hexValue = decimalValue.toString(16).padStart(2, "0");

  export let showAscii: boolean = true;
  export let showHex: boolean = true;
  export let showDecimal: boolean = true;
</script>

<div class="container">
  {#if showAscii}
    <span class="ascii">{asciiValue}</span>
  {/if}
  {#if showHex}
    <span class="hex">{hexValue}</span>
  {/if}
  {#if showDecimal}
    <span class="dec">{decimalValue}</span>
  {/if}
</div>

<style>
  .container {
    width: 32px;
  }

  .container span {
    display: block;
    text-align: right;
    font-family: monospace;
  }

  .ascii {
    background-color: turquoise;
  }

  .hex {
    background-color: lightgreen;
  }

  .dec {
    background-color: lightcoral;
  }
</style>
