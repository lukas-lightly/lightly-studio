<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import X from '@lucide/svelte/icons/x';
    import { Button } from '$lib/components/ui/button';
    import { Input } from '$lib/components/ui/input';
    import { Label } from '$lib/components/ui/label';

    const dispatch = createEventDispatcher();

    let files: FileList;

    function handleDrop(e: DragEvent) {
        if (e.dataTransfer) {
            files = e.dataTransfer.files;
        }
    }
</script>

<div
    class="fixed inset-0 z-50 flex items-center justify-center bg-black/50"
    on:click={() => dispatch('close')}
>
    <div
        class="relative w-full max-w-lg rounded-lg bg-card p-8"
        on:click|stopPropagation
    >
        <Button
            variant="ghost"
            class="absolute right-4 top-4 h-8 w-8 p-0"
            on:click={() => dispatch('close')}
        >
            <X class="h-4 w-4" />
        </Button>
        <div class="flex flex-col gap-4">
            <h2 class="text-lg font-semibold">Image Search</h2>
            <div class="grid w-full items-center gap-1.5">
                <Label for="search">Search</Label>
                <Input id="search" type="text" placeholder="Search for images" />
            </div>
            <div
                class="flex h-32 w-full items-center justify-center rounded-md border-2 border-dashed border-gray-300 bg-gray-50 text-gray-400"
                on:dragover|preventDefault
                on:drop|preventDefault={handleDrop}
            >
                <p>Drag and drop an image here</p>
            </div>
            <div class="grid grid-cols-3 gap-4">
                <!-- Grid for displaying results -->
            </div>
        </div>
    </div>
</div>
