<script>
  // @ts-nocheck
  export let entries;
  import Chip from "./Chip.svelte";
</script>

<div class="m-4">
  {#if entries.length}
    {#each entries as entry}
      <div class="border-2 p-2 text-left mb-4">
        <div class="p-2 border-b-2"><b>Title:</b> {entry.item?.title}</div>
        <div class="h-44 p-2">
          <b>Description:</b>
          {entry.item?.description}
        </div>
        {#each entry.item?.tags as tag}
          <Chip message={tag} />
        {/each}
      </div>
    {/each}
  {:else}
    <span>No data found!</span>
  {/if}
</div>
