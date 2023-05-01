<script>
  import Details from "../components/details.svelte";
  import Nav from "../components/nav.svelte";
  import DisplayOption from "../components/displayOption.svelte";
  import TableCsv from "../components/tableCSV.svelte";
</script>

<div id="whpage" class="flex flex-row sd:flex-col gap-20 h-screen w-screen p-5">
  <Nav />
  <div class="flex flex-col gap-5 basis-4/5">
    <div class="flex flex-col h-1/6 w-1/3 text-blue-t">
      <h1 class="text-2xl">Welcome Jess!</h1>
      <h2 class="text-xl">Lorem ipsum dolor sit amet, consectetur</h2>
    </div>
    <Details />
    <div class="flex flex-row h-1/3 w-full">
      <TableCsv />
      <div class="basis-1/12"></div>
      <div class="basis-1/12"></div>
      <DisplayOption />
    </div>
  </div>
</div>

