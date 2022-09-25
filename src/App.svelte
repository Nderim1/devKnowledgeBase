<script>
  // @ts-nocheck

  import Fuse from "fuse.js";
  import { init } from "svelte/internal";
  import dataJson from "./data.json";
  import DisplayData from "./lib/DisplayData.svelte";
  import Modal from "./lib/Modal.svelte";
  import { writable } from "svelte/store";
  import Popup from "./lib/Popup.svelte";
  import Content from "./lib/Content.svelte";
  const modal = writable(null);
  const showModal = () => modal.set(Popup, { message: "It's a modal!" });

  let searchedValue = "";

  const fuse = new Fuse(dataJson.entries, {
    keys: ["title", "description", "tags"],
    threshold: 0.4,
    minMatchCharLength: 3,
  });
  let searchedEntries = [];

  const initData = () => {
    searchedEntries = dataJson.entries.map((data) => ({
      item: data,
    }));

    searchedValue = "";
  };

  initData();

  const handleSearchChange = (event) => {
    if (event.target.value.length === 0) return initData();
    if (event.target.value.length >= 3)
      searchedEntries = fuse.search(event.target.value);
  };
</script>

<main>
  <div class="m-8">
    <h2 class="text-2xl">Dev knowledge center</h2>
    <span
      >This project aim to be my knoledge center about web information I learn
      during day to day development, code reviews, videos and readings, talking
      with colleagues.</span
    >
    <span
      >The info needs to be added and tagged so it makes it easier to search
      through at a later point.</span
    >
  </div>
  <div class="">
    Search:
    <input
      autofocus
      type="text"
      class="w-96"
      on:input={handleSearchChange}
      bind:value={searchedValue}
    />
    <button on:click={initData}>Clear</button>
    <div class="text-left m-4">
      <Modal show={$modal}>
        <Content />
      </Modal>
    </div>
  </div>
  <DisplayData entries={searchedEntries} />
</main>
