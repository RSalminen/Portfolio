<script lang="ts">
  
  export let classStr = "";
</script>

<p class={classStr + " text-[15px]"}>
  <slot />
</p>
