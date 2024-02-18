<script lang="ts">
    export let href : string;
</script>

<a class="text-blue-700 hover:text-blue-900" href={href} target="_blank"><slot /></a>