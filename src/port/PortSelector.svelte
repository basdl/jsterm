<script lang="ts">
  import { Button } from "carbon-components-svelte";
  import { createEventDispatcher } from "svelte";

  async function selectPort() {
    port = await navigator.serial.requestPort();
    dispatch("portSelected", port);
  }

  async function getPorts() {
    return await navigator.serial.getPorts();
  }

  navigator.serial.addEventListener("connect", (e) => {
    dispatch("newPortConnected", e.target);
  });

  navigator.serial.addEventListener("disconnect", (e) => {
    dispatch("portDisconnected", e.target);
  });

  const dispatch = createEventDispatcher();
  export let ports = getPorts();
  export let port = null;
</script>

<Button size="small" on:click={selectPort}>Select Port</Button>
