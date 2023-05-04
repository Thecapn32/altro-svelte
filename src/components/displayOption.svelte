<script>
    export let dispOption;
</script>

<div id="disop" class="flex flex-col w-1/2 h-full items-center justify-center text-white font-bold text-xl">
    <div class="flex flex-row w-2/3 h-1/3 border border-collapse">
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "A"? "bg-white": ""}"></div>
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "B"? "bg-white": ""}"></div>
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "C"? "bg-white": ""}"></div>
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "D"? "bg-white": ""}"></div>
    </div>
    <div class="flex flex-row w-2/3 h-1/3 border border-collapse">
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "E"? "bg-white": ""}"></div>
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "F"? "bg-white": ""}"></div>
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "G"? "bg-white": ""}"></div>
        <div class="flex flex-col w-1/4 border border-collapse {dispOption == "H"? "bg-white": ""}"></div>
    </div>
</div>