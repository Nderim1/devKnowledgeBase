<script>
  export let message;
  export let removeTag;
  // export let noClose = true;

  let noClose = removeTag ? false : true;
</script>

<span
  class="pt-0 pb-0 pl-2 pr-2 bg-slate-500 m-2 rounded-sm hover:cursor-pointer"
  on:click={(e) => (noClose ? () => {} : removeTag(message))}
>
  {message}
</span>
