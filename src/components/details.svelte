<div id="detail" class="flex flex-col h-1/2 w-full">
    <div class="basis-1/6 p-3 text-detail">  
      <h1>Details</h1>
    </div>
    <div class="flex flex-row basis-1/6">
      <div class="basis-1/2 p-2">
        <label class="block text-sm text-white" for="channel">Channel</label>
        <select id="channel" class="block w-3/4 h-3/4 select-box text-white">
          <option value="CH0">CH0</option>
          <option value="CH1">CH1</option>
          <option value="CH2">CH2</option>
          <option value="CH3">CH3</option>
          <option value="CH4">CH4</option>
          <option value="CH5">CH5</option>
          <option value="CH6">CH6</option>
          <option value="CH7">CH7</option>
      </select>
      </div>
      <div class="basis-1/2 p-2">
        <label class="block text-sm text-white" for="name">Name</label>
        <input id="name" class="w-3/4 h-3/4 select-box placeholder-white text-white" type="text" placeholder="Type here"/>
      </div>
    </div>
    <div class="flex flex-row basis-1/6">
      <div class="basis-1/2 p-2">
        <label class="block text-sm text-white" for="display-option">Display Option</label>
        <select id="display-option" class="w-3/4 h-3/4 select-box text-white">
          <option value="A">A</option>
          <option value="B">B</option>
          <option value="C">C</option>
          <option value="D">D</option>
          <option value="E">E</option>
          <option value="F">F</option>
          <option value="G">G</option>
          <option value="H">H</option>
        </select>
      </div>
      <div class="basis-1/2 p-2">
        <label class="block text-sm text-white" for="display-option">Display Option</label>
        <select class="w-3/4 h-3/4 select-box text-white">
          <option value="Psi">Psi</option>
          <option value="BAR">BAR</option>
          <option value="Celsius">Celsius</option>
          <option value="Fahrenheit">Fahrenheit</option>
          <option value="Lambda">Lambda</option>
          <option value="AFR">AFR</option>
          <option value="Voltage">Voltage</option>
      </select>
      </div>
    </div>
    <div class="flex flex-row basis-1/6">
      <div class="basis-1/2 p-2">
        <label class="block text-sm text-white" for="file">Upload CSV</label>
        <input id="file" class="w-3/4 h-3/4 select-box placeholder-white text-white text-sm file:border-white" type="file" accept=".csv"/>
      </div>
      <div class="flex flex-row basis-1/2 p-2">
        <div class="basis-1/3">
          <label class="block text-sm text-white" for="min">Min</label>
          <input id="min" type="number" class="w-3/4 h-3/4 select-box text-white placeholder-white"/>
        </div>
        <div class="basis-1/3">
          <label class="block text-sm text-white" for="max">Max</label>
          <input id="max" type="number" class="w-3/4 h-3/4 select-box text-white placeholder-white"/>
        </div>
      </div>
    </div>
    <div class="flex flex-row basis-1/6">
      <div class="basis-1/2 p-2">
        <label class="block text-sm text-white" for="ref">Does This Sensor Have 5V Reference</label>
        <select id="ref" class="w-3/4 h-3/4 select-box text-white">
          <option value="yes">Yes</option>
          <option value="no">No</option>
      </select>
      </div>
      <div class="basis-1/2"></div>
    </div>
    <div class="flex flex-row basis-1/6 items-center justify-center">
      <div class="basis-1/4"></div>
      <button class="w-1/4 h-1/2 rounded m-2 bg-white text-slate-800 text-sm hover:bg-sky-500">
        SAVE
      </button>
      <button class="w-1/4 h-1/2 rounded m-2 bg-white text-slate-800 text-sm hover:bg-sky-500">
        PREVIEW
      </button>
      <div class="basis-1/4"></div>
    </div>
  </div>