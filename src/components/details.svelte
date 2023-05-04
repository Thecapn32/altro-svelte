<script>
    import PapaParse from "papaparse";
    import regression from "regression";

    let pageObj = {
        id: 0,
        channel: "CH0",
        unit: "",
        pos: "",
        name: "",
        max: 0,
        min: 0,
        ref: "",
        coeff: [0, 0, 0, 0],
    };

    async function saveInfo() {
        if (
            pageObj.unit == "" ||
            pageObj.max < 0 ||
            pageObj.min < 0 ||
            pageObj.name == "" ||
            pageObj.pos == "" ||
            pageObj.ref == ""
        ) {
            alert("Invalid Field!");
            return;
        }
        const res = await fetch("/save", {
            method: "POST",
            body: JSON.stringify(pageObj),
        });
        const json = await res.json();
        console.log(json);
    }

    async function preview() {
        const res = await fetch("/preview", {
            method: "POST",
            body: pageObj.channel,
        });
        const filterOBJ = await res.json();
        console.log(filterOBJ);
        pageObj.max = filterOBJ.max;
        pageObj.min = filterOBJ.min;
        pageObj.name = filterOBJ.name;
        pageObj.pos = filterOBJ.pos;
        pageObj.unit = filterOBJ.unit;
    }

    let dataToCSV = [];
    let prevDataToCSV;

    export let allowedFileExtensions = ["csv"];

    let maxFileSize = 3145728;

    let uploader;

    function onUpload(file) {
        //console.log("this is csv file", file, file.length - 2);
        const data = [];

        for (let index = 0; index < file.length - 1; index++) {
            data.push([parseFloat(file[index][0]), parseFloat(file[index][1])]);
        }
        //console.log(data);
        const result = regression.polynomial(data, { order: 3 });

        pageObj.coeff[0] = result.equation[0];
        pageObj.coeff[1] = result.equation[1];
        pageObj.coeff[2] = result.equation[2];
        pageObj.coeff[3] = result.equation[3];

        console.log(result.equation);
    }

    function uploadFile(event) {
        event.preventDefault();
        const file = uploader.files[0];

        const fileExtensionArray = file.type.split("/");
        const fileExtension = fileExtensionArray[fileExtensionArray.length - 1];

        if (file.size > maxFileSize) {
            console.log("Above the max file size threshold");
            return;
        }
        if (fileExtension.includes("csv") && file.size < maxFileSize) {
            const csvData = PapaParse.parse(file, {
                complete: (results) => {
                    onUpload
                        ? onUpload(results.data)
                        : console.log(
                              "Remember to define an onUpload function as props. Parsed CSV:",
                              results.data
                          );
                },
            });
        } else if (allowedFileExtensions.includes(fileExtension)) {
            onUpload
                ? onUpload(file)
                : console.log(
                      "Remember to define an onUpload function as props. Plain file:",
                      file
                  );
        } else {
            console.log("Not an allowed file type");
        }
    }

    export let dispOption;

    $: {
        dispOption = pageObj.pos;
    }

    $: {
        // called on props change
        if (dataToCSV !== prevDataToCSV && dataToCSV.length !== 0) {
            prevDataToCSV = dataToCSV;
            const csvData = PapaParse.unparse(dataToCSV);
            const result = regression.polynomial(csvData, { order: 3 });
            console.log("result");
            // console.log(result);
            onUpload
                ? onUpload(csvData)
                : console.log(
                      "Remember to define an onUpload function as props. CSV Data:",
                      csvData
                  );
        }
    }
</script>

<div id="detail" class="flex flex-col h-1/2 w-full">
    <div class="basis-1/12 p-3 text-detail">
        <h1>Details</h1>
    </div>
    <div class="flex flex-row basis-1/6">
        <div class="basis-1/2 p-2">
            <label class="block text-sm text-white" for="channel">Channel</label
            >
            <select
                id="channel"
                class="block w-3/4 h-3/4 select-box text-white"
                bind:value={pageObj.channel}
            >
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
            <input
                id="name"
                class="w-3/4 h-3/4 select-box placeholder-white text-white"
                type="text"
                placeholder="Type here"
                bind:value={pageObj.name}
            />
        </div>
    </div>
    <div class="flex flex-row basis-1/6">
        <div class="basis-1/2 p-2">
            <label class="block text-sm text-white" for="display-option"
                >Display Option</label
            >
            <select
                id="display-option"
                class="w-3/4 h-3/4 select-box text-white"
                bind:value={pageObj.pos}
            >
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
            <label class="block text-sm text-white" for="display-option"
                >Unit</label
            >
            <select
                class="w-3/4 h-3/4 select-box text-white"
                bind:value={pageObj.unit}
            >
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
            <label class="block text-sm text-white" for="file">Upload CSV</label
            >
            <input
                id="file"
                class="w-3/4 h-3/4 select-box placeholder-white text-white text-sm file:border-white"
                type="file"
                accept=".csv"
                bind:this={uploader}
                on:change={uploadFile}
            />
        </div>
        <div class="flex flex-row basis-1/2 p-2">
            <div class="basis-1/3">
                <label class="block text-sm text-white" for="min">Min</label>
                <input
                    id="min"
                    type="number"
                    class="w-3/4 h-3/4 select-box text-white placeholder-white"
                    bind:value={pageObj.min}
                />
            </div>
            <div class="basis-1/3">
                <label class="block text-sm text-white" for="max">Max</label>
                <input
                    id="max"
                    type="number"
                    class="w-3/4 h-3/4 select-box text-white placeholder-white"
                    bind:value={pageObj.max}
                />
            </div>
        </div>
    </div>
    <div class="flex flex-row basis-1/6">
        <div class="basis-1/2 p-2">
            <label class="block text-sm text-white" for="ref"
                >Does This Sensor Have 5V Reference</label
            >
            <select
                id="ref"
                class="w-3/4 h-3/4 select-box text-white"
                bind:value={pageObj.ref}
            >
                <option value="yes">Yes</option>
                <option value="no">No</option>
            </select>
        </div>
        <div class="basis-1/2" />
    </div>
    <div class="flex flex-row basis-1/6 items-center justify-center">
        <div class="basis-1/4" />
        <button
            class="w-1/4 h-1/2 rounded m-2 bg-white text-slate-800 text-sm hover:bg-sky-500"
            on:click={saveInfo}
        >
            SAVE
        </button>
        <button
            class="w-1/4 h-1/2 rounded m-2 bg-white text-slate-800 text-sm hover:bg-sky-500"
            on:click={preview}
        >
            PREVIEW
        </button>
        <div class="basis-1/4" />
    </div>
</div>
