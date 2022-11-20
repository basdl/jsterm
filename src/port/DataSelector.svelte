<script lang="ts">
  import { ComboBox } from "carbon-components-svelte";

  let selectedId = "8";
  export let data: number = parseInt(selectedId);
</script>

<ComboBox
  size="sm"
  titleText="Data"
  placeholder="Select bits per word"
  bind:selectedId
  items={[
    { id: "7", text: "7" },
    { id: "8", text: "8" },
  ]}
/>
