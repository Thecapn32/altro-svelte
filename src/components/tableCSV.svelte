<script>
    let fileTable = 1;
    var inValue = {
        x0: 0,
        y0: 0,
        x1: 0,
        y1: 0,
        x2: 0,
        y2: 0,
    };
</script>

<div id="fileup" class="flex flex-col w-1/3 h-full">
    <div class="flex flex-row basis-1/4">
        <div class="basis-1/2 p-1">
            <button
                class="w-full p-3 rounded {fileTable === 1
                    ? 'bg-sky-500'
                    : 'bg-white'}"
                on:click={() => (fileTable = 1)}
            >
                File
            </button>
        </div>
        <div class="basis-1/2 p-1">
            <button
                class="w-full p-3 rounded {fileTable === 2
                    ? 'bg-sky-500'
                    : 'bg-white'}"
                on:click={() => (fileTable = 2)}
            >
                Table
            </button>
        </div>
    </div>
    <div class="flex flex-row basis-3/4 items-center justify-center p-2">
        {#if fileTable == 1}
            <div
                class="flex items-center justify-center w-full h-full border-2 border-white rounded p-1"
            >
                <button class="w-3/4 h-1/4 rounded bg-white hover:bg-sky-500">
                    Upload
                </button>
            </div>
        {:else if fileTable == 2}
            <div
                class="flex flex-col w-full h-full border-2 border-white rounded p-1"
            >
                <div class="flex flex-row p-2">
                    <label class="block text-sm text-white" for="x0">x[0]</label
                    >
                    <input
                        id="x0"
                        class="select-box placeholder-white text-white w-1/2"
                        type="number"
                        bind:value={inValue.x0}
                    />
                    <label class="block text-sm text-white" for="y0">y[0]</label
                    >
                    <input
                        id="y0"
                        class="select-box placeholder-white text-white w-1/2"
                        type="number"
                        bind:value={inValue.y0}
                    />
                </div>
                <div class="flex flex-row p-2">
                    <label class="block text-sm text-white" for="x1">x[1]</label
                    >
                    <input
                        id="x1"
                        class="select-box placeholder-white text-white w-1/2"
                        type="number"
                        bind:value={inValue.x1}
                    />
                    <label class="block text-sm text-white" for="y1">y[1]</label
                    >
                    <input
                        id="y1"
                        class="select-box placeholder-white text-white w-1/2"
                        type="number"
                        bind:value={inValue.y1}
                    />
                </div>
                <div class="flex flex-row p-2">
                    <label class="block text-sm text-white" for="x2">x[2]</label
                    >
                    <input
                        id="x2"
                        class="select-box placeholder-white text-white w-1/2"
                        type="number"
                        bind:value={inValue.x2}
                    />
                    <label class="block text-sm text-white" for="y2">y[2]</label
                    >
                    <input
                        id="y2"
                        class="select-box placeholder-white text-white w-1/2"
                        type="number"
                        bind:value={inValue.y2}
                    />
                </div>
            </div>
        {/if}
    </div>
</div>
