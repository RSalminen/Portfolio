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

<button class={(sections[isAutoScrolling ? tempIndex : index] === refStr ? "bg-blue-50 text-black pl-8 pr-4 rounded-l-sm flex justify-end" : "pr-16 w-fit") + "py-[1px] transition-all duration-1000"} on:click={() => tempIndex = sections.indexOf(refStr)} use:scrollTo={refStr}>
    {str}
</button>
