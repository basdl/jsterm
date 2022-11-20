<script lang="ts">
  import { Column, Row } from "carbon-components-svelte";
  import { createEventDispatcher } from "svelte";
  import BaudSelector from "./BaudSelector.svelte";
  import DataSelector from "./DataSelector.svelte";
  import type { IPortSettings } from "../helper";
  import ParitySelector from "./ParitySelector.svelte";
  import PortSelector from "./PortSelector.svelte";
  import StopSelector from "./StopSelector.svelte";
  import FlowControlSelector from "./FlowControlSelector.svelte";

  export let settings: IPortSettings = null;
</script>

<PortSelector on:portSelected bind:port={settings.port} />
<BaudSelector bind:baudRate={settings.baudRate} />
<DataSelector bind:data={settings.dataBits} />
<StopSelector bind:data={settings.stopBits} />
<ParitySelector bind:data={settings.parity} />
<FlowControlSelector bind:data={settings.flowControl} />
