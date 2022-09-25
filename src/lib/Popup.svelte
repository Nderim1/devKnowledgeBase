<script>
  // @ts-nocheck
  import Chip from "./Chip.svelte";
  export let message;
  let tagInputValue;
  let tagsAdded = [];

  const handleInputTagKeypress = (e) => {
    if (e.code === "Enter") {
      if (tagsAdded.length > 3) return;
      tagsAdded = tagsAdded.concat(tagInputValue);
      tagInputValue = "";
    }
  };

  const removeTag = (tagToRemove) => {
    console.log("whaaat ----");
    tagsAdded = tagsAdded.filter((tag) => tag !== tagToRemove);
  };
</script>

<div>
  <h2 class="text-2xl">{message}</h2>

  <div class="m-4 flex justify-between">
    <span class="w-36"> Title:</span>
    <input type="text" class="w-full" />
  </div>
  <div class="m-4 flex justify-between">
    <span class="w-36"> Tags:</span>
    <div class="w-full ">
      <input
        type="text"
        class="w-full"
        maxlength="13"
        bind:value={tagInputValue}
        on:keypress={handleInputTagKeypress}
      />
      <!-- <br /> -->
      <div class="m-2">
        {#if !tagsAdded.length}
          none
        {/if}
        {#each tagsAdded as tagAdded}
          <!-- <span class="m-2">{tagAdded}</span> -->
          <Chip message={tagAdded} {removeTag} noClose={false} />
        {/each}
      </div>
    </div>
  </div>
  <div class="m-4 flex justify-between">
    <span class="w-36"> Description:</span>
    <textarea class="w-full" rows="10" />
  </div>
</div>

<style>
</style>
