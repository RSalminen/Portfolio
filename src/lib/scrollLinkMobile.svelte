<script lang="ts">
    import { scrollTo, scrollRef } from 'svelte-scrolling';
    export let str : string;
    export let refStr : string;
    export let index : number;
    export let tempIndex : number;
    export let isAutoScrolling : boolean;

    let sections = [
        'about',
        'projects',
        'contact'
    ]

</script>

<button class={(sections[isAutoScrolling ? tempIndex : index] === refStr ? "border-b-4 border-blue-50" : "")} on:click={() => tempIndex = sections.indexOf(refStr)} use:scrollTo={refStr}>
    {str}
</button>
