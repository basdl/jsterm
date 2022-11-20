<script lang="ts">
  import { ComboBox } from "carbon-components-svelte";

  let selectedId = "none";
  export let data = selectedId;
</script>

<ComboBox
  size="sm"
  titleText="Parity"
  bind:selectedId
  placeholder="Select your parity bit"
  items={[
    { id: "none", text: "None" },
    { id: "even", text: "Even" },
    { id: "odd", text: "Odd" },
  ]}
/>
