<script lang="ts">
  import { onDestroy, onMount } from "svelte";
  import {
    range,
    SPECIALBYTE_BREAK,
    WORD_GAP,
    WORD_WIDTH,
  } from "./helper";
  import WordView from "./WordView.svelte";
  export let bytes = [];
  export let container = null;

  export let showAscii: boolean = true;
  export let showHex: boolean = true;
  export let showDecimal: boolean = true;
  export let autoScroll: boolean = true;

  export let newLineEveryNthCharacter = 16;

  let scrollTimer = null;
  function updateScroller(shouldBeScrolled) {
    clearInterval(scrollTimer);

    if (shouldBeScrolled) {
      scrollTimer = setInterval(() => {
        if (container) {
          container.scrollTop = container.scrollHeight;
        }
      }, 1000);
    }
  }

  $: updateScroller(autoScroll);

  let headerWidth = 0;
  $: headerElements = range(
    1,
    Math.floor(headerWidth / (WORD_WIDTH + WORD_GAP))
  );

  onDestroy(() => {
    clearInterval(scrollTimer);
  });
</script>

<div class="containerHeader" bind:clientWidth={headerWidth}>
  {#each headerElements as ix}
    <div class="headerIndex">{ix}</div>
  {/each}
</div>

<div class="container" bind:this={container}>
  <div class="break" />
  {#each bytes as byte, i}
    {#if byte == SPECIALBYTE_BREAK}
      <div class="break" />
    {:else}
      <WordView decimalValue={byte} {showAscii} {showHex} {showDecimal} />
      {#if (i + 1) % newLineEveryNthCharacter == 0 && newLineEveryNthCharacter > 0}
        <div class="break" />
      {/if}
    {/if}
  {/each}
</div>

<style>
  .container,
  .containerHeader {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    gap: 4px;
  }

  .container {
    height: 30rem;
    overflow-y: scroll;
  }

  .headerIndex {
    width: 32px;
    text-align: right;
    background-color: lightgray;
    font-family: monospace;
  }

  .containerHeader {
    display: flex;
  }

  .break {
    flex-basis: 100%;
    height: 4px;
  }
</style>
