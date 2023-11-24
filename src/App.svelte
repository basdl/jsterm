<script lang="ts">
  import {
    Column,
    Grid,
    InlineNotification,
    Row,
  } from "carbon-components-svelte";
  import MainApp from "./MainApp.svelte";

  let serialPortAvailable = "serial" in navigator;
</script>

{#if serialPortAvailable}
  <MainApp></MainApp>
{:else}
  <Grid>
    <Row>
      <Column></Column>
      <Column>
        <InlineNotification
          hideCloseButton
          kind="warning"
          title="Missing browser support:"
          subtitle="    Serial port is not available on this device / browser. Usually this is
    possible on your PC."
        /></Column
      >
      <Column></Column>
    </Row>
  </Grid>
{/if}
