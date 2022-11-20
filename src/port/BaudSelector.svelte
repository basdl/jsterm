<script lang="ts">
  import { Button, ComboBox } from "carbon-components-svelte";
  import { createEventDispatcher } from "svelte";

  async function selectPort() {
    const port = await navigator.serial.requestPort();
    dispatch("portSelected", port);
    return port;
  }

  let selectedId = "9600";
  export let baudRate: number = parseInt(selectedId);

  const dispatch = createEventDispatcher();
</script>

<ComboBox
  size="sm"
  titleText="Baudrate"
  placeholder="Select your baudrate"
  bind:selectedId
  items={[
    { id: "50", text: "50" },
    { id: "110", text: "110" },
    { id: "150", text: "150" },
    { id: "300", text: "300" },
    { id: "1200", text: "1200" },
    { id: "2400", text: "2400" },
    { id: "4800", text: "4800" },
    { id: "9600", text: "9600" },
    { id: "19200", text: "19200" },
    { id: "38400", text: "38400" },
    { id: "57600", text: "57600" },
    { id: "115200", text: "115200" },
    { id: "230400", text: "230400" },
    { id: "460800", text: "460800" },
    { id: "500000", text: "500000" },
  ]}
/>
