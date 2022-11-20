<script lang="ts">
  import { ComboBox } from "carbon-components-svelte";

  let selectedId = "1";
  export let data: number = parseInt(selectedId);
</script>

<ComboBox
  size="sm"
  titleText="Stop"
  bind:selectedId
  placeholder="Select the amount of stop bits"
  items={[
    { id: "1", text: "1" },
    { id: "2", text: "2" },
  ]}
/>
