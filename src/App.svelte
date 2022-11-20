<script lang="ts">
  import "carbon-components-svelte/css/white.css";
  import {
    Button,
    Checkbox,
    Column,
    Grid,
    Row,
    TextInput,
  } from "carbon-components-svelte";
  import WordsView from "./WordsView.svelte";
  import { IPortSettings, SPECIALBYTE_BREAK } from "./helper";
  import PortSettings from "./port/PortSettings.svelte";

  // Store
  let bytes = [1, 2, 3, 4, 5, 6, 7, 8, 9, 42, 101];
  export let portSettings: IPortSettings = {
    port: null,
    baudRate: 9600,
    dataBits: 8,
    stopBits: 1,
    parity: "none",
    flowControl: "none",
  };
  let showAscii = true;
  let showHex: boolean = true;
  let showDecimal: boolean = true;
  let newLineEveryNthCharacter: number = 0;
  let newLineEveryNMsPause: number = 0;
  let autoScroll: boolean = true;
  let lastReceived = Date.now();

  // Callbacks
  async function onPortSelected() {
    await portSettings.port.open(portSettings);

    await readFromPort((bytes) => {
      bytes.map((b) => newByteReceived(b));
    });
  }

  function clearReceived() {
    bytes = [];
  }

  function newByteReceived(b) {
    const now = Date.now();
    if (now - lastReceived > newLineEveryNMsPause && newLineEveryNMsPause > 0) {
      bytes.push(SPECIALBYTE_BREAK);
    }
    lastReceived = now;
    bytes.push(b);
    bytes = bytes;
  }

  async function readFromPort(cb) {
    while (portSettings.port.readable) {
      const reader = portSettings.port.readable.getReader();
      try {
        while (true) {
          const { value, done } = await reader.read();
          if (done) {
            // |reader| has been canceled.
            break;
          }

          cb(value);
        }
      } catch (error) {
        // Handle |error|...
      } finally {
        reader.releaseLock();
      }
    }
  }

  setInterval(() => {
    //newByteReceived(Math.ceil(Math.random() * 255));
  }, 100);
</script>

<div class="app">
  <div class="sideBar">
    <PortSettings
      bind:settings={portSettings}
      on:portSelected={onPortSelected}
    />
    <TextInput size="sm" labelText="Rx" disabled value={bytes.length} />

    <Button size="small" on:click={clearReceived}>Clear received</Button>
    <Checkbox labelText="Ascii" bind:checked={showAscii} />
    <Checkbox labelText="Hex" bind:checked={showHex} />
    <Checkbox labelText="Dec" bind:checked={showDecimal} />
    <TextInput
      size="sm"
      labelText="Newline every ... char"
      bind:value={newLineEveryNthCharacter}
    />
    <Checkbox labelText="Auto scroll" bind:checked={autoScroll} />
    <TextInput
      size="sm"
      labelText="Newline after ... ms receive pause"
      bind:value={newLineEveryNMsPause}
    />
  </div>
  <div class="wordsView">
    <WordsView
      {bytes}
      {showAscii}
      {showHex}
      {showDecimal}
      {newLineEveryNthCharacter}
      {autoScroll}
    />
  </div>
</div>

<style>
  .sideBar {
    width: 20%;
    padding: 2rem;
  }

  .app {
    display: flex;
    justify-content: space-between;
  }

  .wordsView {
    width: 80%;
    padding: 1rem;
  }
</style>
