<script lang="ts">
  import { ComboBox } from "carbon-components-svelte";

  let selectedId = "none";
  export let data = selectedId;
</script>

<ComboBox
  size="sm"
  bind:selectedId
  titleText="Flow Control"
  placeholder="Select your flow control method"
  items={[
    { id: "none", text: "None" },
    { id: "hardware", text: "Hardware" },
  ]}
/>
