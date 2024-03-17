<script lang="ts">
  
  export let classStr = "";
</script>

<p class={classStr + " text-[14px] md:text-[15px]"}>
  <slot />
</p>
