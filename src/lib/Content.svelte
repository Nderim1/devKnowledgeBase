<script>
  import { getContext } from "svelte";
  import Popup from "./Popup.svelte";
  const { open } = getContext("simple-modal");
  const showModal = () => open(Popup, { message: "Add a new entry" });
</script>

<button on:click={showModal}>Add new entry</button>
