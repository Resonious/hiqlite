<script lang="ts">
    import Button from "$lib/components/Button.svelte";

    let {
        tabs,
        selected = $bindable(''),
        borderRadius = '5px',
        center = false,
        width = 'inherit',
    }: {
        tabs: string[],
        selected: string,
        borderRadius?: string,
        center?: boolean,
        width?: string,
    } = $props();

    if (tabs.length > 0 && selected === '') {
        selected = tabs[0];
    }
</script>

<div
        class="tabs flex gap-05"
        class:center
        style:border-radius={borderRadius}
        style:width
>
    {#each tabs as tab}
        <Button ariaCurrent={tab === selected ? 'step' : undefined} invisible onclick={() => selected = tab}>
            <span class="font-label tab" data-selected={tab === selected}>
                {tab}
            </span>
        </Button>
    {/each}
</div>

<style>
    .tabs {
        padding: .2rem;
        background: hsl(var(--bg-high));
    }

    .center {
        justify-content: center;
    }

    .tab {
        padding: .25rem .5rem;
        border-radius: var(--border-radius);
        color: hsl(var(--text));
        background: hsl(var(--bg-high));
        transition: all 150ms ease-in-out;
    }

    .tab:hover {
        color: hsl(var(--action));
    }

    .tab[data-selected="true"] {
        color: hsl(var(--action));
        background: hsl(var(--bg));
    }
</style>