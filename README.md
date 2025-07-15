<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clinicaide - The Modern Nurse's Toolkit</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-gradient-start: #0f172a;
            --bg-gradient-mid: #1e293b;
            --bg-gradient-end: #334155;
            --text-primary: #f1f5f9;
            --text-secondary: #cbd5e1;
            --text-accent: #94a3b8;
            --glass-bg-main: rgba(30, 41, 59, 0.5);
            --glass-bg-card: rgba(51, 65, 85, 0.6);
            --glass-border: rgba(255, 255, 255, 0.1);
            --blue-accent: #3b82f6;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-image: linear-gradient(135deg, var(--bg-gradient-start) 0%, var(--bg-gradient-mid) 50%, var(--bg-gradient-end) 100%);
            color: var(--text-primary);
            background-attachment: fixed;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg-gradient-end); }
        ::-webkit-scrollbar-thumb { background: rgba(255, 255, 255, 0.2); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(255, 255, 255, 0.3); }

        .modal-content, .calculator-widget {
            background: var(--glass-bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            border-radius: 1rem;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -2px rgba(0,0,0,0.1);
        }

        .modal-content {
             border-radius: 1.5rem;
             box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }
        
        .calculator-widget:hover {
            transform: translateY(-4px) scale(1.02);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.2), 0 10px 10px -5px rgba(0, 0, 0, 0.1);
            border-color: rgba(59, 130, 246, 0.5);
        }

        .gradient-text {
            background-image: linear-gradient(to right, #60a5fa, #c084fc, #fb923c);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .input-glass {
            background: rgba(15, 23, 42, 0.5);
            border: 1px solid var(--glass-border);
            color: var(--text-primary);
            border-radius: 0.5rem;
            transition: all 0.2s ease-in-out;
            padding: 0.75rem 1rem;
        }
        .input-glass:focus {
            outline: none;
            border-color: var(--blue-accent);
            box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.4);
        }
        .input-glass::placeholder {
            color: var(--text-accent);
            opacity: 0.8;
        }
        select.input-glass {
            background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3e%3cpath stroke='%2394a3b8' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='M6 8l4 4 4-4'/%3e%3c/svg%3e");
            background-position: right 0.5rem center;
            background-repeat: no-repeat;
            background-size: 1.5em 1.5em;
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            padding-right: 2.5rem;
        }
        label { color: var(--text-secondary); }
        .input-error-message { color: #f87171; font-size: 0.875rem; }
        .input-error-border { border-color: #f87171 !important; }

        .btn {
            position: relative;
            overflow: hidden;
            transform: translate3d(0, 0, 0);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .btn:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        .btn-primary { background-image: linear-gradient(to right, #3b82f6 0%, #6366f1 100%); color: white; }
        .btn-clear { background: var(--glass-bg-card); border: 1px solid var(--glass-border); color: var(--text-secondary); }
        .btn-clear:hover { background: rgba(51, 65, 85, 0.9); border-color: var(--text-accent); }
        
        .fade-in { animation: fadeIn 0.3s ease-out forwards; }
        .stagger-fade-in { opacity: 0; animation: fadeIn 0.5s ease-out forwards; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .results-card-bg { background-color: rgba(15, 23, 42, 0.3); border: 1px solid var(--glass-border); margin-top: 1.5rem; padding: 1.5rem; border-radius: 0.75rem; box-shadow: inset 0 2px 4px 0 rgba(0,0,0,0.2); }
        .results-strong-text-color { color: #60a5fa; }
        .formula-bg, .breakdown-bg { background-color: rgba(15, 23, 42, 0.5); padding: 0.75rem; border-radius: 0.375rem; border: 1px solid var(--glass-border); color: var(--text-secondary); }
        .interpretation-bg { background-color: rgba(59, 130, 246, 0.2); border: 1px solid rgba(59, 130, 246, 0.4); color: #93c5fd; }
        
        .patient-icon { width: 2.5rem; height: 2.5rem; color: #60a5fa; margin-right: 0.75rem;}

        /* --- VISUALIZATION STYLES --- */
        .donut-chart-track { stroke: rgba(255, 255, 255, 0.1); }
        .donut-chart-value {
            stroke-linecap: round;
            transition: stroke-dashoffset 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .linear-gauge-track { background-color: rgba(255, 255, 255, 0.1); }
        .linear-gauge-pointer {
            transition: left 0.8s cubic-bezier(0.4, 0, 0.2, 1);
            transform: translateX(-50%);
        }
        .bar-chart-grid-line { stroke: rgba(255, 255, 255, 0.1); stroke-dasharray: 2 4; }
        .bar-chart-bar { transition: height 0.8s cubic-bezier(0.4, 0, 0.2, 1); }

    </style>
    <script type="importmap">
    {
      "imports": {
        "@google/genai": "https://esm.sh/@google/genai@^1.5.1"
      }
    }
    </script>
</head>
<body class="bg-slate-900 text-slate-200">

    <div id="app" class="min-h-screen p-4 sm:p-6 lg:p-8">
        <header class="text-center mb-8 sm:mb-12">
            <h1 class="text-4xl sm:text-5xl md:text-6xl font-extrabold tracking-tight gradient-text">
                Clinicaide
            </h1>
            <div class="mt-8 w-full max-w-xl mx-auto">
                 <div class="relative">
                    <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                        <svg class="w-5 h-5 text-text-accent" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                            <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
                        </svg>
                    </div>
                    <input type="search" id="searchInput" placeholder="Search calculators..." class="input-glass block w-full pl-12 pr-4 py-3 border rounded-full shadow-lg">
                </div>
            </div>
        </header>

        <main>
            <div id="calculatorWidgetsHost" class="max-w-7xl mx-auto"></div>
            <div id="no-results" class="text-center p-10 hidden">
                <h2 class="text-2xl font-bold text-text-secondary">No calculators found</h2>
                <p class="text-text-accent mt-2">Try adjusting your search terms.</p>
            </div>
        </main>
    </div>

    <!-- Modal for Calculator -->
    <div id="calculator-modal" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center p-0 sm:p-4 z-50 hidden">
        <div id="modal-content-wrapper" class="modal-content w-full h-full sm:w-full sm:h-auto sm:max-w-3xl sm:max-h-[90vh] flex flex-col transform transition-all duration-300 sm:rounded-2xl">
            <div class="p-5 sm:p-6 border-b border-b-glass-border flex justify-between items-center flex-shrink-0">
                <h2 id="modal-title" class="text-xl sm:text-2xl font-bold gradient-text">Calculator</h2>
                <button id="modal-close-btn" class="p-2 rounded-full text-text-accent hover:bg-white/10 transition">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            <div class="flex-grow overflow-y-auto p-5 sm:p-6">
                 <form id="calculator-form" novalidate>
                    <div id="modal-inputs" class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-5"></div>
                 </form>
                <div id="modal-result-card" class="mt-6 hidden"></div>
            </div>
            <div class="p-5 sm:p-6 border-t border-t-glass-border flex-shrink-0 bg-black/10 rounded-b-none sm:rounded-b-2xl">
                <div class="flex flex-col sm:flex-row space-y-3 sm:space-y-0 sm:space-x-4">
                    <button id="modal-calculate-btn" class="btn btn-primary w-full sm:w-auto flex-grow font-semibold py-3 px-6 rounded-lg shadow-lg">Calculate</button>
                    <button id="modal-clear-btn" class="btn btn-clear w-full sm:w-auto font-semibold py-3 px-6 rounded-lg">Clear</button>
                </div>
            </div>
        </div>
    </div>

<script>
    // Note: Some complex calculators (ASCVD, APACHE II, SOFA, NIHSS) will provide input fields
    // but direct calculation to specialized tools due to their complexity.
    const allCalculatorsData = [
        {
            category: "Unit Conversions",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4" /></svg>`,
            calculators: [
                {
                    id: "tempConverter", name: "Temperature (°C ↔ °F)", widgetType: 'converter',
                    inputs: [ { id: 'celsius', unit: '°C' }, { id: 'fahrenheit', unit: '°F' } ],
                    calculate: function({ value, sourceId }) {
                        if (sourceId === 'celsius') return { fahrenheit: (value * 9/5) + 32 };
                        return { celsius: (value - 32) * 5/9 };
                    }
                },
                {
                    id: "massConverter", name: "Mass (kg ↔ lb)", widgetType: 'converter',
                    inputs: [ { id: 'kg', unit: 'kg' }, { id: 'lb', unit: 'lb' } ],
                    calculate: function({ value, sourceId }) {
                        if (sourceId === 'kg') return { lb: value * 2.20462 };
                        return { kg: value / 2.20462 };
                    }
                },
                {
                    id: "smallMassConverter", name: "Small Mass (g ↔ mg ↔ mcg)", widgetType: 'converter',
                    inputs: [ { id: 'g', unit: 'g' }, { id: 'mg', unit: 'mg' }, { id: 'mcg', unit: 'mcg' }],
                    calculate: function({ value, sourceId }) {
                        if (sourceId === 'g') return { mg: value * 1000, mcg: value * 1000000 };
                        if (sourceId === 'mg') return { g: value / 1000, mcg: value * 1000 };
                        return { g: value / 1000000, mg: value / 1000 };
                    }
                },
                {
                    id: "volumeConverter", name: "Volume (mL ↔ fl oz)", widgetType: 'converter',
                    inputs: [ { id: 'ml', unit: 'mL' }, { id: 'floz', unit: 'fl oz' } ],
                    calculate: function({ value, sourceId }) {
                        if (sourceId === 'ml') return { floz: value / 29.5735 };
                        return { ml: value * 29.5735 };
                    }
                },
                 {
                    id: "kitchenVolumeConverter", name: "Kitchen Vol. (tsp ↔ Tbsp ↔ mL)", widgetType: 'converter',
                    inputs: [ { id: 'tsp', unit: 'tsp' }, { id: 'tbsp', unit: 'Tbsp' }, { id: 'ml_kitchen', unit: 'mL' } ],
                    calculate: function({ value, sourceId }) {
                        if (sourceId === 'tsp') return { tbsp: value / 3, ml_kitchen: value * 4.92892 };
                        if (sourceId === 'tbsp') return { tsp: value * 3, ml_kitchen: value * 14.7868 };
                        return { tsp: value / 4.92892, tbsp: value / 14.7868 };
                    }
                },
                {
                    id: "lengthConverter", name: "Length (cm ↔ in)", widgetType: 'converter',
                    inputs: [ { id: 'cm', unit: 'cm' }, { id: 'inch', unit: 'in' } ],
                    calculate: function({ value, sourceId }) {
                        if (sourceId === 'cm') return { inch: value / 2.54 };
                        return { cm: value * 2.54 };
                    }
                },
                {
                    id: "heightConverter", name: "Height (cm ↔ ft/in)", widgetType: 'converter-special',
                    inputs: [ { id: 'cm_height', unit: 'cm' }, { id: 'ft_height', unit: 'ft' }, { id: 'in_height', unit: 'in' } ],
                    calculate: function({ value, sourceId, allValues }) {
                         if (sourceId === 'cm_height') {
                            const totalInches = value / 2.54;
                            const feet = Math.floor(totalInches / 12);
                            const inches = totalInches % 12;
                            return { ft_height: feet.toFixed(0), in_height: inches.toFixed(1) };
                        } else { // source is ft or in
                            const feet = parseFloat(allValues.ft_height || 0);
                            const inches = parseFloat(allValues.in_height || 0);
                            const totalInches = (feet * 12) + inches;
                            return { cm_height: (totalInches * 2.54).toFixed(1) };
                        }
                    }
                },
            ]
        },
        {
            category: "Foundational Calculations",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" /></svg>`,
            calculators: [
                {
                    id: "medicationDosage",
                    name: "Medication Dosage",
                    inputs: [
                        { id: "desiredDose", label: "Desired Dose (D)", type: "number", unit: "mg", placeholder: "e.g., 750" },
                        { id: "doseOnHand", label: "Dose on Hand (H)", type: "number", unit: "mg", placeholder: "e.g., 250" },
                        { id: "volumeVehicle", label: "Volume/Vehicle (V)", type: "number", unit: "mL or tablets", placeholder: "e.g., 5" }
                    ],
                    outputs: [{ id: "amountToAdminister", label: "Amount to Administer", unit: "mL or tablets" }],
                    formulaText: "X = (D / H) * V",
                    calculate: function(values) {
                        const D = parseFloat(values.desiredDose);
                        const H = parseFloat(values.doseOnHand);
                        const V = parseFloat(values.volumeVehicle);
                        if (isNaN(D) || isNaN(H) || isNaN(V) || H === 0) return { error: "Invalid input. Ensure all fields are numeric and Dose on Hand is not zero." };
                        if (D < 0 || H < 0 || V < 0) return { error: "Inputs must be positive values." };
                        const result = (D / H) * V;
                        return { amountToAdminister: result.toFixed(2) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Desired Dose (D): ${values.desiredDose} ${values.desiredDose_unit || 'mg'}<br>
                            2. Dose on Hand (H): ${values.doseOnHand} ${values.doseOnHand_unit || 'mg'}<br>
                            3. Volume/Vehicle (V): ${values.volumeVehicle} ${values.volumeVehicle_unit || 'mL or tablets'}<br>
                            4. Formula: X = (D / H) * V<br>
                            5. Calculation: (${values.desiredDose} / ${values.doseOnHand}) * ${values.volumeVehicle} = <strong class="results-strong-text-color">${result.amountToAdminister} ${values.volumeVehicle_unit || 'mL or tablets'}</strong>
                        `;
                    }
                },
                {
                    id: "ivFlowRateMlHr",
                    name: "IV Flow Rate (mL/hr)",
                    inputs: [
                        { id: "totalVolume", label: "Total Volume", type: "number", unit: "mL", placeholder: "e.g., 1000" },
                        { id: "totalTimeHours", label: "Total Time", type: "number", unit: "hours", placeholder: "e.g., 8" }
                    ],
                    outputs: [{ id: "flowRateMlHr", label: "Flow Rate", unit: "mL/hr" }],
                    formulaText: "Flow Rate (mL/hr) = Total Volume (mL) / Total Time (hours)",
                    calculate: function(values) {
                        const vol = parseFloat(values.totalVolume);
                        const time = parseFloat(values.totalTimeHours);
                        if (isNaN(vol) || isNaN(time) || time === 0) return { error: "Invalid input. Ensure fields are numeric and time is not zero." };
                        if (vol < 0 || time < 0) return { error: "Inputs must be positive."};
                        const rate = vol / time;
                        return { flowRateMlHr: rate.toFixed(1) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Total Volume: ${values.totalVolume} mL<br>
                            2. Total Time: ${values.totalTimeHours} hours<br>
                            3. Formula: Total Volume / Total Time<br>
                            4. Calculation: ${values.totalVolume} mL / ${values.totalTimeHours} hours = <strong class="results-strong-text-color">${result.flowRateMlHr} mL/hr</strong>
                        `;
                    }
                },
                {
                    id: "ivFlowRateGttMin",
                    name: "IV Flow Rate (gtt/min)",
                    inputs: [
                        { id: "totalVolumeGtt", label: "Total Volume", type: "number", unit: "mL", placeholder: "e.g., 200" },
                        { id: "totalTimeMinutes", label: "Total Time", type: "number", unit: "minutes", placeholder: "e.g., 90" },
                        { id: "dropFactor", label: "Drop Factor", type: "number", unit: "gtt/mL", placeholder: "e.g., 15 (Macro) or 60 (Micro)" }
                    ],
                    outputs: [{ id: "flowRateGttMin", label: "Flow Rate", unit: "gtt/min" }],
                    formulaText: "Flow Rate (gtt/min) = (Total Volume (mL) * Drop Factor (gtt/mL)) / Total Time (minutes)",
                    calculate: function(values) {
                        const vol = parseFloat(values.totalVolumeGtt);
                        const time = parseFloat(values.totalTimeMinutes);
                        const factor = parseFloat(values.dropFactor);
                        if (isNaN(vol) || isNaN(time) || isNaN(factor) || time === 0) return { error: "Invalid input. Ensure fields are numeric and time is not zero." };
                         if (vol < 0 || time < 0 || factor < 0) return { error: "Inputs must be positive."};
                        const rate = (vol * factor) / time;
                        return { flowRateGttMin: Math.round(rate) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Total Volume: ${values.totalVolumeGtt} mL<br>
                            2. Total Time: ${values.totalTimeMinutes} minutes<br>
                            3. Drop Factor: ${values.dropFactor} gtt/mL<br>
                            4. Formula: (Total Volume * Drop Factor) / Total Time<br>
                            5. Calculation: (${values.totalVolumeGtt} mL * ${values.dropFactor} gtt/mL) / ${values.totalTimeMinutes} min = <strong class="results-strong-text-color">${result.flowRateGttMin} gtt/min</strong> (rounded)
                        `;
                    }
                }
            ]
        },
        {
            category: "Adult Health Nursing",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" /></svg>`,
            calculators: [
                {
                    id: "bmi",
                    name: "Body Mass Index (BMI)",
                    visualizationType: "linearGauge", 
                    visualizationParams: {
                        unit: 'kg/m²',
                        ranges: [
                            { label: 'Underweight', max: 18.5, color: '#3b82f6' }, // blue-500
                            { label: 'Normal', max: 24.9, color: '#22c55e' }, // green-500
                            { label: 'Overweight', max: 29.9, color: '#f59e0b' }, // amber-500
                            { label: 'Obesity I', max: 34.9, color: '#ef4444' }, // red-500
                            { label: 'Obesity II', max: 39.9, color: '#a855f7' }, // purple-500
                            { label: 'Obesity III', max: 50, color: '#d946ef' } // fuchsia-500
                        ],
                        displayMin: 10,
                        displayMax: 50
                    },
                    inputs: [
                        { id: "weightKg", label: "Weight", type: "number", unit: "kg", placeholder: "e.g., 70" },
                        { id: "heightCm", label: "Height", type: "number", unit: "cm", placeholder: "e.g., 175" }
                    ],
                    outputs: [{ id: "bmiValue", label: "BMI", unit: "kg/m²" }],
                    formulaText: "BMI = Weight (kg) / (Height (m))²",
                    calculate: function(values) {
                        const weight = parseFloat(values.weightKg);
                        const heightCm = parseFloat(values.heightCm);
                        if (isNaN(weight) || isNaN(heightCm) || heightCm === 0) return { error: "Invalid input. Ensure fields are numeric and height is not zero." };
                        if (weight <= 0 || heightCm <= 0) return { error: "Weight and height must be positive values."};
                        const heightM = heightCm / 100;
                        const bmi = weight / (heightM * heightM);
                        return { bmiValue: bmi.toFixed(1) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        const heightM = parseFloat(values.heightCm) / 100;
                        return `
                            1. Weight: ${values.weightKg} kg<br>
                            2. Height: ${values.heightCm} cm = ${heightM.toFixed(2)} m<br>
                            3. Formula: Weight (kg) / (Height (m))²<br>
                            4. Calculation: ${values.weightKg} kg / (${heightM.toFixed(2)} m)² = <strong class="results-strong-text-color">${result.bmiValue} kg/m²</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const bmi = parseFloat(result.bmiValue);
                        if (bmi < 18.5) return "Category: Underweight. Increased risk of nutritional deficiencies. Normal Range: 18.5-24.9 kg/m².";
                        if (bmi < 25) return "Category: Normal weight. Indicates a healthy weight for height. Normal Range: 18.5-24.9 kg/m².";
                        if (bmi < 30) return "Category: Overweight. Increased risk for chronic diseases. Normal Range: 18.5-24.9 kg/m².";
                        if (bmi < 35) return "Category: Obesity Class I. High risk for chronic diseases. Normal Range: 18.5-24.9 kg/m².";
                        if (bmi < 40) return "Category: Obesity Class II. Very high risk for chronic diseases. Normal Range: 18.5-24.9 kg/m².";
                        return "Category: Obesity Class III. Extremely high risk. Normal Range: 18.5-24.9 kg/m².";
                    }
                },
                {
                    id: "fluidBalance",
                    name: "Fluid Balance (I&O)",
                    visualizationType: "barChart", 
                    inputs: [ 
                        { id: "intakeItems", label: "Intake Items", type: "dynamicList", listName: "Intake" },
                        { id: "outputItems", label: "Output Items", type: "dynamicList", listName: "Output" }
                    ],
                    outputs: [
                        { id: "totalIntake", label: "Total Intake", unit: "mL" },
                        { id: "totalOutput", label: "Total Output", unit: "mL" },
                        { id: "finalBalance", label: "Final Fluid Balance", unit: "mL" }
                    ],
                    formulaText: "Fluid Balance = Total Intake - Total Output",
                    calculate: function(values) {
                        let totalIntake = 0;
                        (values.intakeItems || []).forEach(item => totalIntake += parseFloat(item.amount || 0));
                        let totalOutput = 0;
                        (values.outputItems || []).forEach(item => totalOutput += parseFloat(item.amount || 0));
                        const finalBalance = totalIntake - totalOutput;
                        return {
                            totalIntake: totalIntake.toFixed(0),
                            totalOutput: totalOutput.toFixed(0),
                            finalBalance: finalBalance.toFixed(0)
                        };
                    },
                    getCalculationBreakdown: function(values, result) {
                        let intakeBreakdown = (values.intakeItems || []).map(item => `&nbsp;&nbsp;&nbsp;&nbsp;- ${item.description || 'Unnamed'}: ${item.amount || 0} mL`).join('<br>');
                        let outputBreakdown = (values.outputItems || []).map(item => `&nbsp;&nbsp;&nbsp;&nbsp;- ${item.description || 'Unnamed'}: ${item.amount || 0} mL`).join('<br>');
                        return `
                            1. Total Intake Items:<br>${intakeBreakdown || '&nbsp;&nbsp;&nbsp;&nbsp;- No intake items entered'}<br>
                               <strong class="results-strong-text-color">Total Intake: ${result.totalIntake} mL</strong><br><br>
                            2. Total Output Items:<br>${outputBreakdown || '&nbsp;&nbsp;&nbsp;&nbsp;- No output items entered'}<br>
                               <strong class="results-strong-text-color">Total Output: ${result.totalOutput} mL</strong><br><br>
                            3. Formula: Total Intake - Total Output<br>
                            4. Calculation: ${result.totalIntake} mL - ${result.totalOutput} mL = <strong class="results-strong-text-color">${result.finalBalance >= 0 ? '+' : ''}${result.finalBalance} mL</strong>
                        `;
                    }
                },
                { 
                    id: "creatinineClearanceCGAdult",
                    name: "Creatinine Clearance (Cockcroft-Gault)",
                    inputs: [
                        { id: "ageYearsCG", label: "Age", type: "number", unit: "years", placeholder: "e.g., 65" },
                        { id: "weightCrClCG", label: "Weight (Mass)", type: "number", unit: "kg", placeholder: "e.g., 70" },
                        { id: "serumCreatinineCG", label: "Serum Creatinine", type: "number", unit: "mg/dL", placeholder: "e.g., 1.2" },
                        { id: "genderCG", label: "Gender", type: "select", options: [ {value: "male", text: "Male"}, {value: "female", text: "Female"} ] }
                    ],
                    outputs: [{ id: "crclValueCG", label: "Creatinine Clearance", unit: "mL/min" }],
                    formulaText: "C_Cr = ((140 - Age) * Mass (kg)) / (72 * Serum Creatinine (mg/dL))  (x 0.85 for females)",
                    calculate: function(values) {
                        const age = parseInt(values.ageYearsCG);
                        const weight = parseFloat(values.weightCrClCG);
                        const cr = parseFloat(values.serumCreatinineCG);
                        if (isNaN(age) || isNaN(weight) || isNaN(cr) || cr === 0) return { error: "Invalid input. Ensure fields are numeric and Serum Creatinine is not zero." };
                        if (age <=0 || weight <=0 || cr <=0) return { error: "Age, weight, and serum creatinine must be positive values."};

                        let crcl = ((140 - age) * weight) / (72 * cr);
                        if (values.genderCG === "female") {
                            crcl *= 0.85;
                        }
                        return { crclValueCG: crcl.toFixed(1) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        let femaleMultiplier = values.genderCG === "female" ? " * 0.85 (for female)" : "";
                        return `
                            1. Age: ${values.ageYearsCG} years<br>
                            2. Weight (Mass): ${values.weightCrClCG} kg<br>
                            3. Serum Creatinine: ${values.serumCreatinineCG} mg/dL<br>
                            4. Gender: ${values.genderCG.charAt(0).toUpperCase() + values.genderCG.slice(1)}<br>
                            5. Formula: ((140 - Age) * Mass) / (72 * Serum Creatinine)${femaleMultiplier}<br>
                            6. Calculation: ((140 - ${values.ageYearsCG}) * ${values.weightCrClCG}) / (72 * ${values.serumCreatinineCG})${femaleMultiplier} = <strong class="results-strong-text-color">${result.crclValueCG} mL/min</strong>
                        `;
                    },
                     interpretResult: function(result) { 
                        const crcl = parseFloat(result.crclValueCG);
                        let interpretation = `Estimated CrCl: ${crcl.toFixed(1)} mL/min. This value is used for medication dosage adjustments. `;
                        if (crcl < 15) interpretation += "Represents Stage 5 CKD (Kidney Failure).";
                        else if (crcl < 30) interpretation += "Represents Stage 4 CKD (Severe GFR Decrease).";
                        else if (crcl < 60) interpretation += "Represents Stage 3 CKD (Moderate GFR Decrease).";
                        else if (crcl < 90) interpretation += "Represents Stage 2 CKD (Mild GFR Decrease, if other kidney damage signs present).";
                        else interpretation += "Represents Normal or Stage 1 CKD (if other kidney damage signs present).";
                        return interpretation + " Note: Cockcroft-Gault estimates CrCl, which approximates GFR in stable patients.";
                    }
                },
                { 
                    id: "anionGapGeneralAdult",
                    name: "Anion Gap",
                    visualizationType: "donutChart", 
                    visualizationParams: { 
                        unit: 'mEq/L',
                        maxScore: 25,
                        ranges: [
                            { till: 2, label: 'Low', color: '#f59e0b' },
                            { till: 12, label: 'Normal', color: '#22c55e' },
                            { till: 25, label: 'High', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                        { id: "sodiumAG", label: "Sodium (Na⁺)", type: "number", unit: "mEq/L", placeholder: "e.g., 140" },
                        { id: "chlorideAG", label: "Chloride (Cl⁻)", type: "number", unit: "mEq/L", placeholder: "e.g., 100" },
                        { id: "bicarbonateAG", label: "Bicarbonate (HCO₃⁻)", type: "number", unit: "mEq/L", placeholder: "e.g., 22" }
                    ],
                    outputs: [{ id: "anionGapValue", label: "Anion Gap", unit: "mEq/L" }],
                    formulaText: "Anion Gap = [Na⁺] - ([Cl⁻] + [HCO₃⁻])",
                    calculate: function(values) {
                        const na = parseFloat(values.sodiumAG);
                        const cl = parseFloat(values.chlorideAG);
                        const hco3 = parseFloat(values.bicarbonateAG);
                        if (isNaN(na) || isNaN(cl) || isNaN(hco3)) return { error: "Invalid input. Ensure all fields are numeric." };
                        const gap = na - (cl + hco3);
                        return { anionGapValue: gap.toFixed(0) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Sodium (Na⁺): ${values.sodiumAG} mEq/L<br>
                            2. Chloride (Cl⁻): ${values.chlorideAG} mEq/L<br>
                            3. Bicarbonate (HCO₃⁻): ${values.bicarbonateAG} mEq/L<br>
                            4. Formula: [Na⁺] - ([Cl⁻] + [HCO₃⁻])<br>
                            5. Calculation: ${values.sodiumAG} - (${values.chlorideAG} + ${values.bicarbonateAG}) = <strong class="results-strong-text-color">${result.anionGapValue} mEq/L</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const gap = parseFloat(result.anionGapValue);
                        if (gap > 12) return "Interpretation: High Anion Gap. Suggests metabolic acidosis from causes like DKA, lactic acidosis, or toxins. Normal Range: 3-11 mEq/L (may vary by lab).";
                        if (gap < 3) return "Interpretation: Low Anion Gap. Rare; consider hypoalbuminemia, paraproteinemia, or lab error. Normal Range: 3-11 mEq/L.";
                        return "Interpretation: Normal Anion Gap. If acidosis is present, consider non-anion gap causes. Normal Range: 3-11 mEq/L.";
                    }
                }
            ]
        },
        {
            category: "Pediatric Nursing",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" /></svg>`,
            calculators: [
                {
                    id: "pediatricDosage",
                    name: "Weight-Based Dosage (Peds)",
                    inputs: [
                        { id: "prescribedDosePerKg", label: "Prescribed Dose", type: "number", unit: "mg/kg/day", placeholder: "e.g., 40" },
                        { id: "weightPeds", label: "Weight", type: "number", unit: "kg", placeholder: "e.g., 18" },
                        { id: "dosesPerDay", label: "Number of Doses per day", type: "number", unit: "doses", placeholder: "e.g., 2" }
                    ],
                    outputs: [
                        { id: "totalDailyDose", label: "Total Daily Dose", unit: "mg" },
                        { id: "singleDose", label: "Single Dose", unit: "mg" }
                    ],
                    formulaText: "Total Daily Dose = Prescribed (mg/kg/day) * Weight (kg); Single Dose = Total Daily Dose / Doses per day",
                    calculate: function(values) {
                        const doseKgDay = parseFloat(values.prescribedDosePerKg);
                        const weight = parseFloat(values.weightPeds);
                        const numDoses = parseInt(values.dosesPerDay);
                        if (isNaN(doseKgDay) || isNaN(weight) || isNaN(numDoses) || numDoses === 0) return { error: "Invalid input. Ensure fields are numeric and doses/day is not zero." };
                        if (doseKgDay <= 0 || weight <= 0 || numDoses <= 0) return { error: "All inputs must be positive values."};
                        const totalDaily = doseKgDay * weight;
                        const single = totalDaily / numDoses;
                        return {
                            totalDailyDose: totalDaily.toFixed(2),
                            singleDose: single.toFixed(2)
                        };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Prescribed Dose: ${values.prescribedDosePerKg} mg/kg/day<br>
                            2. Weight: ${values.weightPeds} kg<br>
                            3. Number of Doses per day: ${values.dosesPerDay}<br><br>
                            4. Calculate Total Daily Dose:<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Formula: Prescribed Dose * Weight<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Calculation: ${values.prescribedDosePerKg} mg/kg/day * ${values.weightPeds} kg = <strong class="results-strong-text-color">${result.totalDailyDose} mg/day</strong><br><br>
                            5. Calculate Single Dose:<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Formula: Total Daily Dose / Number of Doses per day<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Calculation: ${result.totalDailyDose} mg/day / ${values.dosesPerDay} doses = <strong class="results-strong-text-color">${result.singleDose} mg/dose</strong>
                        `;
                    }
                },
                {
                    id: "maintenanceFluidsPeds",
                    name: "Maintenance Fluid (Holliday-Segar)",
                    inputs: [
                        { id: "weightFluidsPeds", label: "Weight", type: "number", unit: "kg", placeholder: "e.g., 15" }
                    ],
                    outputs: [
                        { id: "total24hrFluid", label: "Total 24-hour Fluid Need", unit: "mL" },
                        { id: "hourlyRateFluid", label: "Hourly Rate", unit: "mL/hr" }
                    ],
                    formulaText: "100mL/kg for 1st 10kg; 50mL/kg for next 10kg (11-20kg); 20mL/kg for each kg >20kg.",
                    calculate: function(values) {
                        const weight = parseFloat(values.weightFluidsPeds);
                        if (isNaN(weight) || weight <= 0) return { error: "Invalid input. Weight must be a positive number." };

                        let fluid = 0;
                        if (weight <= 10) {
                            fluid = weight * 100;
                        } else if (weight <= 20) {
                            fluid = (10 * 100) + ((weight - 10) * 50);
                        } else {
                            fluid = (10 * 100) + (10 * 50) + ((weight - 20) * 20);
                        }
                        const hourlyRate = fluid / 24;
                        return {
                            total24hrFluid: fluid.toFixed(0),
                            hourlyRateFluid: hourlyRate.toFixed(1)
                        };
                    },
                    getCalculationBreakdown: function(values, result) {
                        const weight = parseFloat(values.weightFluidsPeds);
                        let breakdown = `1. Weight: ${weight} kg<br><br>2. Calculation Steps (Holliday-Segar Method):<br>`;
                        let fluidCalc = "";
                        if (weight <= 10) {
                            fluidCalc = `&nbsp;&nbsp;&nbsp;&nbsp;- First 10 kg: ${weight.toFixed(1)} kg * 100 mL/kg = ${(weight * 100).toFixed(0)} mL<br>`;
                        } else if (weight <= 20) {
                            fluidCalc = `&nbsp;&nbsp;&nbsp;&nbsp;- First 10 kg: 10 kg * 100 mL/kg = 1000 mL<br>`;
                            fluidCalc += `&nbsp;&nbsp;&nbsp;&nbsp;- Next ${ (weight - 10).toFixed(1) } kg (up to 20kg): ${(weight - 10).toFixed(1)} kg * 50 mL/kg = ${((weight - 10) * 50).toFixed(0)} mL<br>`;
                        } else {
                            fluidCalc = `&nbsp;&nbsp;&nbsp;&nbsp;- First 10 kg: 10 kg * 100 mL/kg = 1000 mL<br>`;
                            fluidCalc += `&nbsp;&nbsp;&nbsp;&nbsp;- Next 10 kg (11-20kg): 10 kg * 50 mL/kg = 500 mL<br>`;
                            fluidCalc += `&nbsp;&nbsp;&nbsp;&nbsp;- Remaining ${ (weight - 20).toFixed(1) } kg: ${(weight - 20).toFixed(1)} kg * 20 mL/kg = ${((weight - 20) * 20).toFixed(0)} mL<br>`;
                        }
                        breakdown += fluidCalc;
                        breakdown += `<br>3. Total 24-hour Fluid Need: <strong class="results-strong-text-color">${result.total24hrFluid} mL</strong><br>`;
                        breakdown += `4. Hourly Rate: ${result.total24hrFluid} mL / 24 hours = <strong class="results-strong-text-color">${result.hourlyRateFluid} mL/hr</strong>`;
                        return breakdown;
                    }
                },
                {
                    id: "minUrineOutputPeds",
                    name: "Minimum Urine Output (Peds)",
                    inputs: [
                        { id: "weightUrinePeds", label: "Weight", type: "number", unit: "kg", placeholder: "e.g., 12" },
                        { id: "shiftDuration", label: "Duration of Shift", type: "number", unit: "hours", placeholder: "e.g., 8" }
                    ],
                    outputs: [{ id: "minUrineOutput", label: "Minimum Urine Output for Shift", unit: "mL" }],
                    formulaText: "Min Urine Output (mL) = Weight (kg) * 1 mL/kg/hr * Duration (hours) (typical for older children; 1.5-2 mL/kg/hr for infants)",
                    calculate: function(values) {
                        const weight = parseFloat(values.weightUrinePeds);
                        const duration = parseFloat(values.shiftDuration);
                        const ratePerKgHr = 1; 
                        if (isNaN(weight) || isNaN(duration)) return { error: "Invalid input. Ensure fields are numeric." };
                        if (weight <= 0 || duration <= 0) return { error: "Weight and duration must be positive values."};
                        const output = weight * ratePerKgHr * duration;
                        return { minUrineOutput: output.toFixed(1) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        const ratePerKgHr = 1; 
                        return `
                            1. Weight: ${values.weightUrinePeds} kg<br>
                            2. Duration of Shift: ${values.shiftDuration} hours<br>
                            3. Assumed Minimum Rate: ${ratePerKgHr} mL/kg/hr (Note: Infants may require 1.5-2 mL/kg/hr)<br>
                            4. Formula: Weight * Rate * Duration<br>
                            5. Calculation: ${values.weightUrinePeds} kg * ${ratePerKgHr} mL/kg/hr * ${values.shiftDuration} hours = <strong class="results-strong-text-color">${result.minUrineOutput} mL</strong>
                        `;
                    }
                }
            ]
        },
        {
            category: "Obstetric Nursing",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" /><path stroke-linecap="round" stroke-linejoin="round" d="M12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" transform="scale(0.5) translate(12 24)"/></svg>`,
            calculators: [
                {
                    id: "eddNaegeles",
                    name: "Estimated Date of Delivery (Naegele's Rule)",
                    inputs: [
                        { id: "lmpDate", label: "First Day of Last Menstrual Period (LMP)", type: "date" }
                    ],
                    outputs: [{ id: "edd", label: "Estimated Date of Delivery (EDD)", unit: "" }],
                    formulaText: "EDD = (LMP - 3 Months) + 7 Days + 1 Year",
                    calculate: function(values) {
                        const lmp = values.lmpDate;
                        if (!lmp) return { error: "Please select the LMP date."};
                        const lmpDate = new Date(lmp + "T00:00:00"); 

                        lmpDate.setMonth(lmpDate.getMonth() - 3);
                        lmpDate.setDate(lmpDate.getDate() + 7);
                        lmpDate.setFullYear(lmpDate.getFullYear() + 1);
                        
                        return { edd: lmpDate.toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' }) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        const lmpDate = new Date(values.lmpDate + "T00:00:00");
                        const initialLmpString = lmpDate.toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' });

                        const step1Date = new Date(lmpDate);
                        step1Date.setMonth(step1Date.getMonth() - 3);
                        const step1String = step1Date.toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' });

                        const step2Date = new Date(step1Date);
                        step2Date.setDate(step2Date.getDate() + 7);
                        const step2String = step2Date.toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' });
                        
                        return `
                            1. First Day of LMP: ${initialLmpString}<br>
                            2. Subtract 3 Months: ${initialLmpString} - 3 Months = ${step1String}<br>
                            3. Add 7 Days: ${step1String} + 7 Days = ${step2String}<br>
                            4. Add 1 Year: ${step2String} + 1 Year = <strong class="results-strong-text-color">${result.edd}</strong>
                        `;
                    }
                },
                {
                    id: "apgarScore",
                    name: "APGAR Score",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 10,
                        ranges: [
                            { till: 3, label: 'Severely Depressed', color: '#ef4444' },
                            { till: 6, label: 'Mildly Depressed', color: '#f59e0b' },
                            { till: 10, label: 'Normal', color: '#22c55e' }
                        ]
                    },
                    inputs: [
                        { id: "appearance", label: "Appearance (Color)", type: "select", options: [ {value: "2", text: "Completely Pink (2)"}, {value: "1", text: "Body Pink, Extremities Blue (Acrocyanosis) (1)"}, {value: "0", text: "Blue, Pale (0)"} ] },
                        { id: "pulse", label: "Pulse (Heart Rate)", type: "select", options: [ {value: "2", text: "> 100 bpm (2)"}, {value: "1", text: "< 100 bpm (1)"}, {value: "0", text: "Absent (0)"} ] },
                        { id: "grimace", label: "Grimace (Reflex Irritability)", type: "select", options: [ {value: "2", text: "Cries, Coughs, Sneezes (Vigorous) (2)"}, {value: "1", text: "Grimace (1)"}, {value: "0", text: "No Response (0)"} ] },
                        { id: "activity", label: "Activity (Muscle Tone)", type: "select", options: [ {value: "2", text: "Active Motion (Well Flexed) (2)"}, {value: "1", text: "Some Flexion of Extremities (1)"}, {value: "0", text: "Limp, Flaccid (0)"} ] },
                        { id: "respirationApgar", label: "Respiration (Breathing Effort)", type: "select", options: [ {value: "2", text: "Good, Strong Cry (2)"}, {value: "1", text: "Slow, Irregular, Weak Cry (1)"}, {value: "0", text: "Absent (0)"} ] }
                    ],
                    outputs: [{ id: "totalApgar", label: "Total APGAR Score", unit: "/ 10" }],
                    formulaText: "Sum of scores for Appearance, Pulse, Grimace, Activity, and Respiration.",
                    calculate: function(values) {
                        const score = parseInt(values.appearance || 0) + parseInt(values.pulse || 0) + parseInt(values.grimace || 0) + parseInt(values.activity || 0) + parseInt(values.respirationApgar || 0);
                        return { totalApgar: score };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Appearance: ${values.appearance} points<br>
                            2. Pulse: ${values.pulse} points<br>
                            3. Grimace: ${values.grimace} points<br>
                            4. Activity: ${values.activity} points<br>
                            5. Respiration: ${values.respirationApgar} points<br>
                            6. Total Score: ${values.appearance} + ${values.pulse} + ${values.grimace} + ${values.activity} + ${values.respirationApgar} = <strong class="results-strong-text-color">${result.totalApgar}</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const score = parseInt(result.totalApgar);
                        if (score >= 7) return "Interpretation: Normal (Score 7-10). Indicates good adaptation; requires routine care.";
                        if (score >= 4) return "Interpretation: Mildly Depressed (Score 4-6). Some assistance for breathing may be required (e.g., stimulation, oxygen).";
                        return "Interpretation: Severely Depressed (Score 0-3). Requires immediate, and possibly extensive, resuscitation.";
                    }
                },
                {
                    id: "bishopScore",
                    name: "Bishop Score",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 13,
                        ranges: [
                            { till: 5, label: 'Unfavorable', color: '#ef4444' },
                            { till: 7, label: 'Moderately Favorable', color: '#f59e0b' },
                            { till: 13, label: 'Favorable', color: '#22c55e' }
                        ]
                    },
                    inputs: [
                        { id: "dilation", label: "Dilation (cm)", type: "select", options: [ {value: "0", text: "Closed (0)"}, {value: "1", text: "1-2 cm (1)"}, {value: "2", text: "3-4 cm (2)"}, {value: "3", text: "≥ 5 cm (3)"} ] },
                        { id: "effacement", label: "Effacement (%)", type: "select", options: [ {value: "0", text: "0-30% (0)"}, {value: "1", text: "40-50% (1)"}, {value: "2", text: "60-70% (2)"}, {value: "3", text: "≥ 80% (3)"} ] },
                        { id: "station", label: "Fetal Station", type: "select", options: [ {value: "0", text: "-3 (0)"}, {value: "1", text: "-2 (1)"}, {value: "2", text: "-1, 0 (2)"}, {value: "3", text: "+1, +2 (3)"} ] },
                        { id: "consistency", label: "Cervical Consistency", type: "select", options: [ {value: "0", text: "Firm (0)"}, {value: "1", text: "Medium (1)"}, {value: "2", text: "Soft (2)"} ] },
                        { id: "position", label: "Cervical Position", type: "select", options: [ {value: "0", text: "Posterior (0)"}, {value: "1", text: "Mid-position (1)"}, {value: "2", text: "Anterior (2)"} ] }
                    ],
                    outputs: [{ id: "totalBishop", label: "Total Bishop Score", unit: "/ 13" }],
                    formulaText: "Sum of scores for Dilation, Effacement, Station, Consistency, and Position.",
                    calculate: function(values) {
                        const score = parseInt(values.dilation || 0) + parseInt(values.effacement || 0) + parseInt(values.station || 0) + parseInt(values.consistency || 0) + parseInt(values.position || 0);
                        return { totalBishop: score };
                    },
                    getCalculationBreakdown: function(values, result) {
                         return `
                            1. Dilation: ${values.dilation} points<br>
                            2. Effacement: ${values.effacement} points<br>
                            3. Station: ${values.station} points<br>
                            4. Consistency: ${values.consistency} points<br>
                            5. Position: ${values.position} points<br>
                            6. Total Score: ${values.dilation} + ${values.effacement} + ${values.station} + ${values.consistency} + ${values.position} = <strong class="results-strong-text-color">${result.totalBishop}</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const score = parseInt(result.totalBishop);
                        if (score >= 8) return "Interpretation: Favorable Cervix (Score ≥ 8). High likelihood of successful induction of labor.";
                        if (score >= 6) return "Interpretation: Moderately Favorable Cervix (Score 6-7). Induction may be successful.";
                        return "Interpretation: Unfavorable Cervix (Score ≤ 5). Cervical ripening agents may be considered before induction.";
                    }
                }
            ]
        },
        { 
            category: "Critical Care (General)",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M4 4v5l4-2.5L12 9V4l-4 2.5L4 4zM4 15l4-2.5L12 15v5l-4-2.5L4 20v-5zM12 4v5l4 2.5L20 9V4l-4 2.5L12 4zM12 15l4 2.5L20 15v5l-4-2.5L12 20v-5z"/></svg>`,
            calculators: [
                { 
                    id: "mapGeneralCritCare",
                    name: "Mean Arterial Pressure (MAP)",
                    inputs: [
                        { id: "sbpMap", label: "Systolic Blood Pressure (SBP)", type: "number", unit: "mmHg", placeholder: "e.g., 120" },
                        { id: "dbpMap", label: "Diastolic Blood Pressure (DBP)", type: "number", unit: "mmHg", placeholder: "e.g., 80" }
                    ],
                    outputs: [{ id: "mapValue", label: "MAP", unit: "mmHg" }],
                    formulaText: "MAP = (SBP + 2 * DBP) / 3",
                    calculate: function(values) {
                        const sbp = parseFloat(values.sbpMap);
                        const dbp = parseFloat(values.dbpMap);
                        if (isNaN(sbp) || isNaN(dbp)) return { error: "Invalid input. Ensure SBP and DBP are numeric." };
                        if (sbp <= 0 || dbp <= 0) return { error: "SBP and DBP must be positive values."};
                        if (sbp < dbp) return { error: "SBP should typically be greater than or equal to DBP."};
                        const mapVal = (sbp + (2 * dbp)) / 3;
                        return { mapValue: mapVal.toFixed(1) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Systolic BP (SBP): ${values.sbpMap} mmHg<br>
                            2. Diastolic BP (DBP): ${values.dbpMap} mmHg<br>
                            3. Formula: (SBP + 2 * DBP) / 3<br>
                            4. Calculation: (${values.sbpMap} + 2 * ${values.dbpMap}) / 3 = <strong class="results-strong-text-color">${result.mapValue} mmHg</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const mapVal = parseFloat(result.mapValue);
                        if (mapVal < 65) return "Interpretation: MAP < 65 mmHg may indicate inadequate organ perfusion. This is a common minimum target in critical care to ensure blood flow to vital organs.";
                        return "Interpretation: MAP ≥ 65 mmHg is generally desired for adequate organ perfusion. Normal range in healthy adults is typically 70-100 mmHg.";
                    }
                },
                { 
                    id: "gcsGeneralCritCare",
                    name: "Glasgow Coma Scale (GCS)",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 15,
                        ranges: [
                            { till: 8, label: 'Severe Injury', color: '#ef4444' },
                            { till: 12, label: 'Moderate Injury', color: '#f59e0b' },
                            { till: 15, label: 'Mild Injury', color: '#22c55e' }
                        ]
                    },
                    inputs: [
                        { id: "eyeOpeningGCS", label: "Eye Opening Response", type: "select", options: [ {value: "4", text: "Spontaneous (4)"}, {value: "3", text: "To Speech (3)"}, {value: "2", text: "To Pain (2)"}, {value: "1", text: "No Response (1)"} ] },
                        { id: "verbalResponseGCS", label: "Verbal Response", type: "select", options: [ {value: "5", text: "Oriented (5)"}, {value: "4", text: "Confused (4)"}, {value: "3", text: "Inappropriate Words (3)"}, {value: "2", text: "Incomprehensible Sounds (2)"}, {value: "1", text: "No Response (1)"} ] },
                        { id: "motorResponseGCS", label: "Motor Response", type: "select", options: [ {value: "6", text: "Obeys Commands (6)"}, {value: "5", text: "Localizes Pain (5)"}, {value: "4", text: "Withdraws from Pain (4)"}, {value: "3", text: "Abnormal Flexion (Decorticate) (3)"}, {value: "2", text: "Abnormal Extension (Decerebrate) (2)"}, {value: "1", text: "No Response (Flaccid) (1)"} ] }
                    ],
                    outputs: [{ id: "totalGcs", label: "Total GCS Score", unit: "/ 15" }],
                    formulaText: "Sum of scores for Eye Opening, Verbal Response, and Motor Response.",
                    calculate: function(values) {
                        const score = parseInt(values.eyeOpeningGCS || 0) + parseInt(values.verbalResponseGCS || 0) + parseInt(values.motorResponseGCS || 0);
                        return { totalGcs: score };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Eye Opening: ${values.eyeOpeningGCS} points<br>
                            2. Verbal Response: ${values.verbalResponseGCS} points<br>
                            3. Motor Response: ${values.motorResponseGCS} points<br>
                            4. Total Score: ${values.eyeOpeningGCS} + ${values.verbalResponseGCS} + ${values.motorResponseGCS} = <strong class="results-strong-text-color">${result.totalGcs}</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const score = parseInt(result.totalGcs);
                        if (score <= 8) return "Severity: Severe Head Injury (GCS ≤ 8). Often requires intubation for airway protection.";
                        if (score <= 12) return "Severity: Moderate Head Injury (GCS 9-12). Requires close monitoring for deterioration.";
                        return "Severity: Mild Head Injury (GCS 13-15). Patient is conscious but may be confused. Max Score: 15.";
                    }
                },
                {
                    id: "parklandFormula",
                    name: "Parkland Formula (Burn Resuscitation)",
                    inputs: [
                        { id: "weightBurn", label: "Weight", type: "number", unit: "kg", placeholder: "e.g., 75" },
                        { id: "tbsa", label: "Total Body Surface Area Burned", type: "number", unit: "%", placeholder: "e.g., 40" }
                    ],
                    outputs: [
                        { id: "totalFluid24hr", label: "Total Fluid in 24 hrs", unit: "mL" },
                        { id: "fluidFirst8hr", label: "Fluid for First 8 hrs", unit: "mL" },
                        { id: "rateFirst8hr", label: "Rate for First 8 hrs", unit: "mL/hr" },
                        { id: "fluidNext16hr", label: "Fluid for Next 16 hrs", unit: "mL" },
                        { id: "rateNext16hr", label: "Rate for Next 16 hrs", unit: "mL/hr" }
                    ],
                    formulaText: "Total Fluid (mL) = 4 mL * Weight (kg) * %TBSA. Give 1st half over 8 hrs, 2nd half over next 16 hrs.",
                    calculate: function(values) {
                        const weight = parseFloat(values.weightBurn);
                        const tbsa = parseFloat(values.tbsa);
                        if (isNaN(weight) || isNaN(tbsa)) return { error: "Invalid input. Ensure fields are numeric." };
                        if (weight <= 0 || tbsa < 0 || tbsa > 100) return { error: "Weight must be positive. TBSA must be between 0 and 100."};

                        const totalFluid = 4 * weight * tbsa;
                        const first8hrFluid = totalFluid / 2;
                        const next16hrFluid = totalFluid / 2;
                        const rate8hr = first8hrFluid / 8;
                        const rate16hr = next16hrFluid / 16;

                        return {
                            totalFluid24hr: totalFluid.toFixed(0),
                            fluidFirst8hr: first8hrFluid.toFixed(0),
                            rateFirst8hr: rate8hr.toFixed(0),
                            fluidNext16hr: next16hrFluid.toFixed(0),
                            rateNext16hr: rate16hr.toFixed(0)
                        };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Weight: ${values.weightBurn} kg<br>
                            2. %TBSA Burned: ${values.tbsa} %<br><br>
                            3. Total Fluid in 24 hours:<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Formula: 4 mL * Weight (kg) * %TBSA<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Calculation: 4 mL * ${values.weightBurn} kg * ${values.tbsa}% = <strong class="results-strong-text-color">${result.totalFluid24hr} mL</strong><br><br>
                            4. Fluid for First 8 Hours (from time of burn):<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Volume: ${result.totalFluid24hr} mL / 2 = <strong class="results-strong-text-color">${result.fluidFirst8hr} mL</strong><br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Rate: ${result.fluidFirst8hr} mL / 8 hours = <strong class="results-strong-text-color">${result.rateFirst8hr} mL/hr</strong><br><br>
                            5. Fluid for Next 16 Hours:<br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Volume: ${result.totalFluid24hr} mL / 2 = <strong class="results-strong-text-color">${result.fluidNext16hr} mL</strong><br>
                               &nbsp;&nbsp;&nbsp;&nbsp;Rate: ${result.fluidNext16hr} mL / 16 hours = <strong class="results-strong-text-color">${result.rateNext16hr} mL/hr</strong>
                        `;
                    }
                },
                {
                    id: "cpp",
                    name: "Cerebral Perfusion Pressure (CPP)",
                    inputs: [
                        { id: "mapForCpp", label: "Mean Arterial Pressure (MAP)", type: "number", unit: "mmHg", placeholder: "e.g., 85" },
                        { id: "icp", label: "Intracranial Pressure (ICP)", type: "number", unit: "mmHg", placeholder: "e.g., 15" }
                    ],
                    outputs: [{ id: "cppValue", label: "CPP", unit: "mmHg" }],
                    formulaText: "CPP = MAP - ICP",
                    calculate: function(values) {
                        const mapVal = parseFloat(values.mapForCpp);
                        const icpVal = parseFloat(values.icp); 
                        if (isNaN(mapVal) || isNaN(icpVal)) return { error: "Invalid input. Ensure MAP and ICP are numeric." };
                         if (mapVal <= 0 || icpVal < 0) return { error: "MAP must be positive, ICP non-negative."}; 
                        const cppResult = mapVal - icpVal; 
                        return { cppValue: cppResult.toFixed(1) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        return `
                            1. Mean Arterial Pressure (MAP): ${values.mapForCpp} mmHg<br>
                            2. Intracranial Pressure (ICP): ${values.icp} mmHg<br>
                            3. Formula: MAP - ICP<br>
                            4. Calculation: ${values.mapForCpp} mmHg - ${values.icp} mmHg = <strong class="results-strong-text-color">${result.cppValue} mmHg</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const cppVal = parseFloat(result.cppValue);
                        let interp = `CPP: ${cppVal.toFixed(1)} mmHg. `;
                        if (cppVal < 50) interp += "Critical brain hypoperfusion; brain ischemia is likely.";
                        else if (cppVal < 60) interp += "Low; monitor closely as this is below the target for many patients, increasing ischemia risk.";
                        else if (cppVal <= 70) interp += "Adequate for most brain injury patients; this is a common target range.";
                        else interp += "Above typical target; monitor for potential hyperperfusion or increased ICP.";
                        return interp + " Normal ICP: 5-15 mmHg. Target CPP is usually 60-70 mmHg, but varies by patient.";
                    }
                },
                {
                    id: "pfRatio",
                    name: "PaO₂/FiO₂ Ratio (P/F Ratio)",
                    visualizationType: "linearGauge",
                    visualizationParams: {
                        unit: '',
                        ranges: [
                            { label: 'Severe ARDS', max: 100, color: '#ef4444' }, // red-500
                            { label: 'Moderate ARDS', max: 200, color: '#f97316' }, // orange-500
                            { label: 'Mild ARDS', max: 300, color: '#f59e0b' }, // amber-500
                            { label: 'Normal', max: 500, color: '#22c55e' } // green-500
                        ],
                        displayMin: 0,
                        displayMax: 500
                    },
                    inputs: [
                        { id: "pao2", label: "PaO₂ (Arterial Oxygen Partial Pressure)", type: "number", unit: "mmHg", placeholder: "e.g., 90" },
                        { id: "fio2", label: "FiO₂ (Fraction of Inspired Oxygen)", type: "number", unit: "%", placeholder: "e.g., 60 (for 60%)" }
                    ],
                    outputs: [{ id: "pfRatioValue", label: "P/F Ratio", unit: "" }],
                    formulaText: "P/F Ratio = PaO₂ / (FiO₂ / 100)",
                    calculate: function(values) {
                        const pao2Val = parseFloat(values.pao2); 
                        const fio2Percent = parseFloat(values.fio2);
                        if (isNaN(pao2Val) || isNaN(fio2Percent) || fio2Percent === 0) return { error: "Invalid input. Ensure fields are numeric and FiO₂ is not zero." };
                        if (pao2Val < 0 || fio2Percent < 21 || fio2Percent > 100) return { error: "PaO2 must be non-negative. FiO2 must be between 21% and 100%."};
                        const fio2Decimal = fio2Percent / 100;
                        const ratio = pao2Val / fio2Decimal;
                        return { pfRatioValue: ratio.toFixed(0) };
                    },
                    getCalculationBreakdown: function(values, result) {
                        const fio2Decimal = parseFloat(values.fio2) / 100;
                        return `
                            1. PaO₂: ${values.pao2} mmHg<br>
                            2. FiO₂: ${values.fio2}% = ${fio2Decimal.toFixed(2)} (as decimal)<br>
                            3. Formula: PaO₂ / FiO₂ (decimal)<br>
                            4. Calculation: ${values.pao2} mmHg / ${fio2Decimal.toFixed(2)} = <strong class="results-strong-text-color">${result.pfRatioValue}</strong>
                        `;
                    },
                    interpretResult: function(result) {
                        const ratio = parseFloat(result.pfRatioValue);
                        if (ratio <= 100) return "ARDS Severity (Berlin Criteria): Severe (P/F Ratio ≤ 100).";
                        if (ratio <= 200) return "ARDS Severity (Berlin Criteria): Moderate (100 < P/F Ratio ≤ 200).";
                        if (ratio <= 300) return "ARDS Severity (Berlin Criteria): Mild (200 < P/F Ratio ≤ 300).";
                        return "Interpretation: Normal oxygenation or Acute Lung Injury not meeting ARDS criteria (P/F Ratio > 300).";
                    }
                }
            ]
        },
        {
            category: "Cardiology",
            categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 016.364 0L12 7.636l1.318-1.318a4.5 4.5 0 116.364 6.364L12 20.364l-7.682-7.682a4.5 4.5 0 010-6.364z" /></svg>`,
            calculators: [
                {
                    id: "ascvdRiskScore", name: "ASCVD Risk Score",
                    inputs: [ 
                        {id: "ageASCVD", label:"Age", type:"number", unit:"years"}, {id: "totalCholesterolASCVD", label:"Total Cholesterol", type:"number", unit:"mg/dL"}, {id:"hdlASCVD", label:"HDL Cholesterol", type:"number", unit:"mg/dL"} 
                    ],
                    outputs: [{id:"ascvdInfo", label:"ASCVD Risk Information"}],
                    formulaText: "Complex algorithm including Age, Sex, Race, TC, HDL, SBP, BP Meds, Diabetes, Smoking.",
                    infoMessage: "The ASCVD Risk Score is complex and best calculated using a dedicated, validated clinical tool. This calculator provides a general overview of factors.",
                    calculate: function(values){ return {info: "Refer to a specialized ACC/AHA ASCVD risk estimator tool for accurate calculation."}; },
                    getCalculationBreakdown: function(values,result){ return `This score considers multiple factors: Age (${values.ageASCVD || 'N/A'}), Total Cholesterol (${values.totalCholesterolASCVD || 'N/A'}), HDL (${values.hdlASCVD || 'N/A'}), and others not listed here.`; },
                },
                {
                    id: "chadsVascScore", name: "CHA₂DS₂-VASc Score",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 9,
                        ranges: [
                            { till: 0, label: 'Very Low Risk', color: '#22c55e' },
                            { till: 1, label: 'Low-Mod. Risk', color: '#f59e0b' },
                            { till: 9, label: 'Mod-High Risk', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                        {id: "chf", label:"Congestive Heart Failure", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "hypertension", label:"Hypertension", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "ageChads", label:"Age", type:"select", options:[{value:"0", text:"<65 (0)"},{value:"1", text:"65-74 (1)"},{value:"2", text:">=75 (2)"}]},
                        {id: "diabetes", label:"Diabetes Mellitus", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "strokeTia", label:"Prior Stroke/TIA/Thromboembolism", type:"select", options:[{value:"0", text:"No (0)"},{value:"2", text:"Yes (2)"}]},
                        {id: "vascularDisease", label:"Vascular Disease (MI, PAD, Aortic Plaque)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "sexCategory", label:"Sex Category (Female)", type:"select", options:[{value:"0", text:"Male (0)"},{value:"1", text:"Female (1)"}]},
                    ],
                    outputs: [{id:"chadsVascTotal", label:"CHA₂DS₂-VASc Score", unit: "/ 9"}],
                    formulaText: "C(1) H(1) A₂(2) D(1) S₂(2) V(1) A(1) Sc(1). Sum of points.",
                    calculate: function(values){ const s = parseInt(values.chf||0)+parseInt(values.hypertension||0)+parseInt(values.ageChads||0)+parseInt(values.diabetes||0)+parseInt(values.strokeTia||0)+parseInt(values.vascularDisease||0)+parseInt(values.sexCategory||0); return {chadsVascTotal: s};},
                    getCalculationBreakdown: function(values,result){ return `CHF: ${values.chf||0}, HTN: ${values.hypertension||0}, Age: ${values.ageChads||0}, DM: ${values.diabetes||0}, Stroke/TIA: ${values.strokeTia||0}, Vasc Dz: ${values.vascularDisease||0}, Sex (Female): ${values.sexCategory||0}.<br>Total = <strong class="results-strong-text-color">${result.chadsVascTotal}</strong>`; },
                    interpretResult: function(result, values) {
                        const score = parseInt(result.chadsVascTotal);
                        const isFemale = values.sexCategory === "1";
                        if (score === 0) return "Risk: Very Low. Antithrombotic therapy is not recommended.";
                        if (score === 1 && isFemale) return "Risk: Low. The single point is from female sex. Antithrombotic therapy is not recommended.";
                        if (score === 1 && !isFemale) return "Risk: Low-Moderate. Oral anticoagulation (OAC) may be considered over aspirin or no therapy. Consult guidelines.";
                        if (score >= 2) return "Risk: Moderate-High. Oral anticoagulation (OAC) is recommended. Consult latest clinical guidelines.";
                        return "Consult clinical guidelines for management recommendations.";
                    }
                },
                {
                    id: "correctedQT", name: "Corrected QT Interval (QTc - Bazett)",
                    inputs: [ 
                        {id: "qtInterval", label:"QT Interval", type:"number", unit:"sec", placeholder:"e.g., 0.40"},
                        {id: "rrInterval", label:"RR Interval", type:"number", unit:"sec", placeholder:"e.g., 1.0"}
                    ],
                    outputs: [{id:"qtcValue", label:"QTc (Bazett)", unit:"ms"}],
                    formulaText: "QTc = QT Interval / √(RR Interval)",
                    calculate: function(values){ const qt = parseFloat(values.qtInterval); const rr = parseFloat(values.rrInterval); if(isNaN(qt) || isNaN(rr) || rr <= 0) return {error: "Invalid QT or RR interval."}; const qtc = (qt / Math.sqrt(rr)) * 1000; return {qtcValue: qtc.toFixed(0)};},
                    getCalculationBreakdown: function(values,result){ return `QT: ${values.qtInterval}s, RR: ${values.rrInterval}s.<br>QTc = ${values.qtInterval} / √${values.rrInterval} = <strong class="results-strong-text-color">${result.qtcValue} ms</strong>`; },
                    interpretResult: function(result){ const qtc = parseFloat(result.qtcValue); if (qtc > 500) return `Severely Prolonged QTc (${qtc}ms). High risk of Torsades de Pointes.`; if(qtc > 460) return `Prolonged QTc (${qtc}ms). Increased risk of Torsades de Pointes.`; if(qtc > 440) return `Borderline QTc (${qtc}ms). Normal is <440ms (males), <460ms (females).`; return `Normal QTc (${qtc}ms).`;}
                },
                {
                    id: "mapCardio", name: "Mean Arterial Pressure (MAP)",
                    inputs: [
                        { id: "sbpMapCardio", label: "Systolic Blood Pressure (SBP)", type: "number", unit: "mmHg", placeholder: "e.g., 120" },
                        { id: "dbpMapCardio", label: "Diastolic Blood Pressure (DBP)", type: "number", unit: "mmHg", placeholder: "e.g., 80" }
                    ],
                    outputs: [{ id: "mapValueCardio", label: "MAP", unit: "mmHg" }],
                    formulaText: "MAP = (SBP + 2 * DBP) / 3",
                    calculate: function(values){ const sbp = parseFloat(values.sbpMapCardio); const dbp = parseFloat(values.dbpMapCardio); if(isNaN(sbp)||isNaN(dbp)||sbp<=0||dbp<=0||sbp<dbp) return {error:"Invalid BP"}; return {mapValueCardio:((sbp+2*dbp)/3).toFixed(1)};},
                    getCalculationBreakdown: function(values,r){ return `SBP: ${values.sbpMapCardio}, DBP: ${values.dbpMapCardio}.<br>(${values.sbpMapCardio} + 2*${values.dbpMapCardio})/3 = <strong class="results-strong-text-color">${r.mapValueCardio} mmHg</strong>`; },
                    interpretResult: function(r){ const map = parseFloat(r.mapValueCardio); if (map < 65) return "MAP < 65 mmHg may indicate inadequate organ perfusion."; return "MAP ≥ 65 mmHg generally desired.";}
                }
            ]
        },
        {
            category: "Pulmonology & Critical Care", categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2h1a2 2 0 002-2v-1a2 2 0 012-2h1.945M7.881 4.006C9.062 5.234 9.974 6.77 9.974 8.5c0 1.51-1.35 2.5-1.35 2.5L3 11V4.006zM21 11h-1.945a2 2 0 00-2 2v1a2 2 0 01-2 2h-1a2 2 0 01-2-2v-1a2 2 0 00-2-2H4.055m13.824-6.994C14.938 5.234 14.026 6.77 14.026 8.5c0 1.51 1.35 2.5 1.35 2.5L21 11V4.006z" /></svg>`,
            calculators: [
                {id: "apacheIIScore", name: "APACHE II Score", inputs: [{id:"apacheParam1", label:"Sample APACHE Parameter", type:"text"}], outputs:[{id:"apacheIIInfo", label:"APACHE II Score Information"}], infoMessage:"APACHE II is a complex ICU scoring system. Use a dedicated validated tool.", formulaText:"Score based on 12 physiological variables, age, and chronic health.", calculate: function(v){return {info:"Refer to specialized tool for APACHE II."}}, getCalculationBreakdown: function(v,r){ return "Requires multiple physiological inputs (temp, MAP, HR, RR, O2, pH, Na, K, Cr, Hct, WBC, GCS), age, and chronic health status.";}},
                {id: "curb65Score", name: "CURB-65 Score",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 5,
                        ranges: [
                            { till: 1, label: 'Low Severity', color: '#22c55e' },
                            { till: 2, label: 'Mod. Severity', color: '#f59e0b' },
                            { till: 5, label: 'High Severity', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                        {id: "confusionCURB", label:"Confusion (new)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "bunCURB", label:"BUN", type:"number", unit:"mg/dL", placeholder:">19 mg/dL is 1 point"},
                        {id: "rrCURB", label:"Respiratory Rate", type:"number", unit:"breaths/min", placeholder:">=30 is 1 point"},
                        {id: "bpCURB", label:"Blood Pressure (SBP<90 or DBP≤60)", type:"select", options:[{value:"0", text:"Normal (0)"},{value:"1", text:"Low (1)"}]},
                        {id: "ageCURB", label:"Age ≥ 65 years", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                    ], outputs:[{id:"curb65Total", label:"CURB-65 Score", unit: "/ 5"}], formulaText:"C(1) U(1) R(1) B(1) 65(1). Sum points.", 
                    calculate: function(v){ let s=0; s+=parseInt(v.confusionCURB||0); if(parseFloat(v.bunCURB)>19)s+=1; if(parseInt(v.rrCURB)>=30)s+=1; s+=parseInt(v.bpCURB||0); s+=parseInt(v.ageCURB||0); if(v.bunCURB===''||isNaN(parseFloat(v.bunCURB)) || v.rrCURB===''||isNaN(parseInt(v.rrCURB))) return {error:"BUN and Respiratory Rate are required."}; return {curb65Total:s}; }, 
                    getCalculationBreakdown: function(v,r){ return `Confusion: ${v.confusionCURB||0}, Urea(BUN>19): ${parseFloat(v.bunCURB)>19?1:0}, RR(≥30): ${parseInt(v.rrCURB)>=30?1:0}, BP(low): ${v.bpCURB||0}, Age(≥65): ${v.ageCURB||0}.<br>Total = <strong class="results-strong-text-color">${r.curb65Total}</strong>`;}, 
                    interpretResult:function(r){ const s = r.curb65Total; if(s<=1) return "Low severity (Score 0-1). Consider outpatient treatment for community-acquired pneumonia."; if(s===2) return "Moderate severity (Score 2). Consider hospital admission."; return "High severity (Score ≥3). Urgent hospital admission, consider ICU assessment.";}},
                {id: "percRule", name: "PERC Rule (PE Rule-out Criteria)", 
                    inputs: [
                        {id: "agePERC", label:"Age ≥ 50 years?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "hrPERC", label:"Heart rate ≥ 100 bpm?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "o2SatPERC", label:"O₂ saturation on room air < 95%?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "vteHistoryPERC", label:"Prior VTE history?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "surgeryTraumaPERC", label:"Recent surgery/trauma (last 4 wks)?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "hemoptysisPERC", label:"Hemoptysis?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "estrogenPERC", label:"Exogenous estrogen use?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                        {id: "legSwellingPERC", label:"Unilateral leg swelling?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]},
                    ], outputs:[{id:"percOutcome", label:"PERC Rule Outcome"}], formulaText:"If ALL criteria are 'No', PE is less likely in low-risk patients.", 
                    calculate: function(v){const criteriaNotMet = Object.values(v).some(val => val === "yes"); return {percOutcome: criteriaNotMet ? "One or more criteria met (PERC rule CANNOT rule out PE)" : "All criteria NOT met (PE less likely if pre-test probability is low)"};}, 
                    getCalculationBreakdown: function(v,r){ let breakdown = "Criteria Check:<br>"; for(const key in v) { breakdown += `${key.replace('PERC','')} : ${v[key]}<br>`; } breakdown += `<strong class="results-strong-text-color">${r.percOutcome}</strong>`; return breakdown;}, 
                    interpretResult:function(r){ return "This rule is for LOW-RISK patients. If PE cannot be ruled out by PERC, further testing (e.g., D-dimer, CTPA) may be needed.";}},
                {id: "sirsCriteria", name: "SIRS Criteria", 
                    inputs: [
                        {id: "tempSIRS", label:"Temperature (°C)", type:"number", placeholder:"<36 or >38"},
                        {id: "hrSIRS", label:"Heart Rate (bpm)", type:"number", placeholder:">90"},
                        {id: "rrSIRS", label:"Respiratory Rate (breaths/min)", type:"number", placeholder:">20"},
                        {id: "paco2SIRS", label:"PaCO₂ (mmHg)", type:"number", placeholder:"<32 (alternative to RR)"},
                        {id: "wbcSIRS", label:"WBC (cells/mm³)", type:"number", placeholder:"<4000 or >12000"},
                        {id: "bandsSIRS", label:"Immature Bands (%)", type:"number", placeholder:">10% (alternative to WBC)"},
                    ], outputs:[{id:"sirsCount", label:"SIRS Criteria Met"}, {id:"sirsDiagnosis", label:"SIRS Diagnosis"}], formulaText:"Two or more of: Temp (<36/>38), HR(>90), RR(>20) or PaCO2(<32), WBC(<4k/>12k) or Bands(>10%).", 
                    calculate: function(v){ let c=0; const t=parseFloat(v.tempSIRS); if(!isNaN(t)&&(t<36||t>38))c++; if(!isNaN(parseInt(v.hrSIRS))&&parseInt(v.hrSIRS)>90)c++; if((!isNaN(parseInt(v.rrSIRS))&&parseInt(v.rrSIRS)>20)||(!isNaN(parseFloat(v.paco2SIRS))&&parseFloat(v.paco2SIRS)<32))c++; if((!isNaN(parseFloat(v.wbcSIRS))&&(parseFloat(v.wbcSIRS)<4||parseFloat(v.wbcSIRS)>12))||(!isNaN(parseFloat(v.bandsSIRS))&&parseFloat(v.bandsSIRS)>10))c++; return{sirsCount:c, sirsDiagnosis:c>=2?"SIRS Likely Present":"SIRS Not Met"}; }, 
                    getCalculationBreakdown: function(v,r){ return `Criteria met: ${r.sirsCount}. Diagnosis: <strong class="results-strong-text-color">${r.sirsDiagnosis}</strong>`;}, 
                    interpretResult:function(r){ return "SIRS indicates systemic inflammation. If due to infection, it's sepsis. SIRS criteria are now less emphasized; consider qSOFA/SOFA for sepsis assessment.";}},
                {id: "sofaScoreCalc", name: "SOFA Score", inputs: [{id:"sofaParam1", label:"Sample SOFA Parameter", type:"text"}], outputs:[{id:"sofaInfo", label:"SOFA Score Information"}], infoMessage:"SOFA score assesses organ dysfunction in ICU. Use a dedicated validated tool.", formulaText:"Score based on Respiration, Coagulation, Liver, CV, CNS, Renal function.", calculate: function(v){return {info:"Refer to specialized tool for SOFA."}}, getCalculationBreakdown: function(v,r){return "Requires PaO2/FiO2, Platelets, Bilirubin, MAP/vasopressors, GCS, Creatinine/Urine Output.";}}
            ]
        },
        {
            category: "Neurology", categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M9 8h6M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>`,
            calculators: [
                {id: "abcd2Score", name: "ABCD² Score for TIA",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 7,
                        ranges: [
                            { till: 3, label: 'Low Risk', color: '#22c55e' },
                            { till: 5, label: 'Moderate Risk', color: '#f59e0b' },
                            { till: 7, label: 'High Risk', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                        {id: "ageABCD2", label:"Age ≥ 60 years", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "bpABCD2", label:"BP (SBP≥140 or DBP≥90)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "clinicalFeaturesABCD2", label:"Clinical Features", type:"select", options:[{value:"0", text:"Other (0)"},{value:"1", text:"Speech disturbance w/o weakness (1)"},{value:"2", text:"Unilateral weakness (2)"}]},
                        {id: "durationABCD2", label:"Duration of Symptoms", type:"select", options:[{value:"0", text:"<10 min (0)"},{value:"1", text:"10-59 min (1)"},{value:"2", text:"≥60 min (2)"}]},
                        {id: "diabetesABCD2", label:"Diabetes", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                    ], outputs:[{id:"abcd2Total", label:"ABCD² Score", unit: "/ 7"}], formulaText:"A(1) B(1) C(1/2) D(1/2) D(1). Sum points.", 
                    calculate: function(v){const s=parseInt(v.ageABCD2||0)+parseInt(v.bpABCD2||0)+parseInt(v.clinicalFeaturesABCD2||0)+parseInt(v.durationABCD2||0)+parseInt(v.diabetesABCD2||0); return {abcd2Total:s};}, 
                    getCalculationBreakdown: function(v,r){return `Age: ${v.ageABCD2||0}, BP: ${v.bpABCD2||0}, Clinical: ${v.clinicalFeaturesABCD2||0}, Duration: ${v.durationABCD2||0}, Diabetes: ${v.diabetesABCD2||0}.<br>Total = <strong class="results-strong-text-color">${r.abcd2Total}</strong>`;}, 
                    interpretResult:function(r){ const s = r.abcd2Total; if(s<=3) return "Low risk of stroke (Score 0-3). 2-day stroke risk is ~1%."; if(s<=5) return "Moderate risk of stroke (Score 4-5). 2-day stroke risk is ~4%. Hospital observation may be justified."; return "High risk of stroke (Score 6-7). 2-day stroke risk is ~8%. Hospital admission is strongly considered.";}},
                {id: "gcsNeuro", name: "Glasgow Coma Scale (GCS)",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 15,
                        ranges: [
                            { till: 8, label: 'Severe Injury', color: '#ef4444' },
                            { till: 12, label: 'Moderate Injury', color: '#f59e0b' },
                            { till: 15, label: 'Mild Injury', color: '#22c55e' }
                        ]
                    },
                    inputs: [
                        { id: "eyeOpeningNeuroGCS", label: "Eye Opening Response", type: "select", options: [ {value: "4", text: "Spontaneous (4)"}, {value: "3", text: "To Speech (3)"}, {value: "2", text: "To Pain (2)"}, {value: "1", text: "No Response (1)"} ] },
                        { id: "verbalResponseNeuroGCS", label: "Verbal Response", type: "select", options: [ {value: "5", text: "Oriented (5)"}, {value: "4", text: "Confused (4)"}, {value: "3", text: "Inappropriate Words (3)"}, {value: "2", text: "Incomprehensible Sounds (2)"}, {value: "1", text: "No Response (1)"} ] },
                        { id: "motorResponseNeuroGCS", label: "Motor Response", type: "select", options: [ {value: "6", text: "Obeys Commands (6)"}, {value: "5", text: "Localizes Pain (5)"}, {value: "4", text: "Withdraws from Pain (4)"}, {value: "3", text: "Abnormal Flexion (Decorticate) (3)"}, {value: "2", text: "Abnormal Extension (Decerebrate) (2)"}, {value: "1", text: "No Response (Flaccid) (1)"} ] }
                    ], outputs:[{id:"totalGcsNeuro", label:"Total GCS Score", unit: "/ 15"}], formulaText:"Sum of E, V, M scores.", 
                    calculate: function(v){const s=parseInt(v.eyeOpeningNeuroGCS||0)+parseInt(v.verbalResponseNeuroGCS||0)+parseInt(v.motorResponseNeuroGCS||0); return {totalGcsNeuro:s};}, 
                    getCalculationBreakdown: function(v,r){ return `Eye: ${v.eyeOpeningNeuroGCS||0}, Verbal: ${v.verbalResponseNeuroGCS||0}, Motor: ${v.motorResponseNeuroGCS||0}.<br>Total = <strong class="results-strong-text-color">${r.totalGcsNeuro}</strong>`;}, 
                    interpretResult:function(r){const score = parseInt(r.totalGcsNeuro); if (score <= 8) return "Severe Head Injury."; if (score <= 12) return "Moderate Head Injury."; return "Mild Head Injury.";}},
                {id: "nihssScore", name: "NIH Stroke Scale (NIHSS)", inputs: [{id:"nihssParam1", label:"Sample NIHSS Item", type:"text"}], outputs:[{id:"nihssInfo", label:"NIHSS Information"}], infoMessage:"NIHSS is a detailed neurologic exam for stroke. Requires certified training and a specific tool/form.", formulaText:"15-item neurologic exam; score 0-42.", calculate: function(v){return {info:"Refer to certified training/tool for NIHSS."}}, getCalculationBreakdown: function(v,r){return "Assesses LOC, Gaze, Visual, Facial Palsy, Motor Arm/Leg, Ataxia, Sensory, Language, Dysarthria, Extinction/Inattention.";}}
            ]
        },
        {
            category: "Nephrology & General Medicine", categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547a2 2 0 00-.547 1.806l.477 2.387a6 6 0 00.517 3.86l.158.318a6 6 0 003.86.517l2.387.477a2 2 0 001.806-.547a2 2 0 00.547-1.806l-.477-2.387a6 6 0 00-.517-3.86l-.158-.318a6 6 0 01-.517-3.86l.477-2.387a2 2 0 00.547-1.806z" /></svg>`,
            calculators: [
                {id: "anionGapNephrology", name: "Anion Gap",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: 'mEq/L',
                        maxScore: 25,
                        ranges: [
                            { till: 2, label: 'Low', color: '#f59e0b' },
                            { till: 12, label: 'Normal', color: '#22c55e' },
                            { till: 25, label: 'High', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                         { id: "sodiumNephroAG", label: "Sodium (Na⁺)", type: "number", unit: "mEq/L", placeholder: "e.g., 140" },
                        { id: "chlorideNephroAG", label: "Chloride (Cl⁻)", type: "number", unit: "mEq/L", placeholder: "e.g., 100" },
                        { id: "bicarbonateNephroAG", label: "Bicarbonate (HCO₃⁻)", type: "number", unit: "mEq/L", placeholder: "e.g., 22" }
                    ], outputs:[{id:"anionGapValueNephro", label:"Anion Gap", unit: "mEq/L"}], formulaText:"[Na⁺] - ([Cl⁻] + [HCO₃⁻])", 
                    calculate: function(v){const na=parseFloat(v.sodiumNephroAG),cl=parseFloat(v.chlorideNephroAG),hco3=parseFloat(v.bicarbonateNephroAG); if(isNaN(na)||isNaN(cl)||isNaN(hco3))return{error:"Invalid numerics"}; return {anionGapValueNephro:(na-(cl+hco3)).toFixed(0)};}, 
                    getCalculationBreakdown: function(v,r){ return `Na: ${v.sodiumNephroAG}, Cl: ${v.chlorideNephroAG}, HCO3: ${v.bicarbonateNephroAG}.<br>${v.sodiumNephroAG} - (${v.chlorideNephroAG} + ${v.bicarbonateNephroAG}) = <strong class="results-strong-text-color">${r.anionGapValueNephro} mEq/L</strong>`;}, 
                    interpretResult:function(r){ const gap = parseFloat(r.anionGapValueNephro); if (gap > 12) return "High Anion Gap. Suggests metabolic acidosis. Normal: 3-11 mEq/L."; if (gap < 3) return "Low Anion Gap. Rare. Normal: 3-11 mEq/L."; return "Normal Anion Gap.";}},
                {id: "creatinineClearanceNephrology", name: "Creatinine Clearance (Cockcroft-Gault)", 
                    inputs: [
                        { id: "ageYearsNephro", label: "Age", type: "number", unit: "years", placeholder: "e.g., 65" },
                        { id: "weightCrClNephro", label: "Weight (Mass)", type: "number", unit: "kg", placeholder: "e.g., 70" },
                        { id: "serumCreatinineNephro", label: "Serum Creatinine", type: "number", unit: "mg/dL", placeholder: "e.g., 1.2" },
                        { id: "genderNephro", label: "Gender", type: "select", options: [ {value: "male", text: "Male"}, {value: "female", text: "Female"} ] }
                    ], outputs:[{id:"crclValueNephro", label:"Creatinine Clearance", unit: "mL/min"}], formulaText:"((140 - Age) * Mass) / (72 * Cr) (x0.85 if female)", 
                    calculate: function(v){ const age=parseInt(v.ageYearsNephro),w=parseFloat(v.weightCrClNephro),cr=parseFloat(v.serumCreatinineNephro); if(isNaN(age)||isNaN(w)||isNaN(cr)||cr===0||age<=0||w<=0||cr<=0) return{error:"Invalid inputs"}; let crcl=((140-age)*w)/(72*cr); if(v.genderNephro==="female")crcl*=0.85; return {crclValueNephro:crcl.toFixed(1)};}, 
                    getCalculationBreakdown: function(v,r){ return `Age: ${v.ageYearsNephro}, Wt: ${v.weightCrClNephro}, SCr: ${v.serumCreatinineNephro}, Gender: ${v.genderNephro}.<br>Calculated Value = <strong class="results-strong-text-color">${r.crclValueNephro} mL/min</strong>`;}, 
                    interpretResult:function(r){ const crcl = parseFloat(r.crclValueNephro); if (crcl < 15) return "Stage 5 CKD."; else if (crcl < 30) return "Stage 4 CKD."; else if (crcl < 60) return "Stage 3 CKD."; else if (crcl < 90) return "Stage 2 CKD (if other kidney damage signs present)."; return "Normal or Stage 1 CKD (if other kidney damage signs present).";}}
            ]
        },
        {
            category: "Gastroenterology & Hepatology", categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2h1a2 2 0 002-2v-1a2 2 0 012-2h1.945M7.881 4.006C9.062 5.234 9.974 6.77 9.974 8.5c0 1.51-1.35 2.5-1.35 2.5L3 11V4.006zM21 11h-1.945a2 2 0 00-2 2v1a2 2 0 01-2 2h-1a2 2 0 01-2-2v-1a2 2 0 00-2-2H4.055m13.824-6.994C14.938 5.234 14.026 6.77 14.026 8.5c0 1.51 1.35 2.5 1.35 2.5L21 11V4.006z" transform="rotate(90 12 12)"/></svg>`,
            calculators: [
                {id: "childPughScore", name: "Child-Pugh Score",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 15,
                        ranges: [
                            { till: 6, label: 'Class A', color: '#22c55e' },
                            { till: 9, label: 'Class B', color: '#f59e0b' },
                            { till: 15, label: 'Class C', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                        {id: "bilirubinChild", label:"Total Bilirubin (mg/dL)", type:"select", options:[{value:"1",text:"<2 (1)"},{value:"2",text:"2-3 (2)"},{value:"3",text:">3 (3)"}]},
                        {id: "albuminChild", label:"Serum Albumin (g/dL)", type:"select", options:[{value:"1",text:">3.5 (1)"},{value:"2",text:"2.8-3.5 (2)"},{value:"3",text:"<2.8 (3)"}]},
                        {id: "inrChild", label:"INR", type:"select", options:[{value:"1",text:"<1.7 (1)"},{value:"2",text:"1.7-2.3 (2)"},{value:"3",text:">2.3 (3)"}]},
                        {id: "ascitesChild", label:"Ascites", type:"select", options:[{value:"1",text:"None (1)"},{value:"2",text:"Mild (Slight) (2)"},{value:"3",text:"Moderate to Severe (Tense) (3)"}]},
                        {id: "encephalopathyChild", label:"Hepatic Encephalopathy", type:"select", options:[{value:"1",text:"None (1)"},{value:"2",text:"Grade 1-2 (Mild) (2)"},{value:"3",text:"Grade 3-4 (Severe) (3)"}]},
                    ], outputs:[{id:"childPughTotal", label:"Child-Pugh Score", unit: "/ 15"}, {id:"childPughClass", label:"Child-Pugh Class"}], formulaText:"Sum of points for Bili, Alb, INR, Ascites, Enceph.", 
                    calculate: function(v){const s = parseInt(v.bilirubinChild||0)+parseInt(v.albuminChild||0)+parseInt(v.inrChild||0)+parseInt(v.ascitesChild||0)+parseInt(v.encephalopathyChild||0); let c=""; if(s<=6)c="Class A"; else if(s<=9)c="Class B"; else c="Class C"; return {childPughTotal:s, childPughClass:c};}, 
                    getCalculationBreakdown: function(v,r){return `Bili: ${v.bilirubinChild||0}, Alb: ${v.albuminChild||0}, INR: ${v.inrChild||0}, Ascites: ${v.ascitesChild||0}, Enceph: ${v.encephalopathyChild||0}.<br>Total = <strong class="results-strong-text-color">${r.childPughTotal} (${r.childPughClass})</strong>`;}, 
                    interpretResult:function(r){return `Score: ${r.childPughTotal}, Class: ${r.childPughClass}. Class A (5-6): Least severe liver disease (1-yr survival ~100%). Class B (7-9): Moderately severe (1-yr survival ~80%). Class C (10-15): Most severe (1-yr survival ~45%).`;}},
                {id: "meldScore", name: "MELD Score", 
                    inputs: [
                        {id: "creatinineMELD", label:"Serum Creatinine", type:"number", unit:"mg/dL"},
                        {id: "bilirubinMELD", label:"Total Bilirubin", type:"number", unit:"mg/dL"},
                        {id: "inrMELD", label:"INR", type:"number"},
                        {id: "sodiumMELD", label:"Serum Sodium (optional for MELD-Na context)", type:"number", unit:"mEq/L", placeholder:"Optional"},
                        {id: "onDialysisMELD", label:"On Dialysis (at least twice in last week)?", type:"select", options:[{value:"no", text:"No"},{value:"yes", text:"Yes"}]}
                    ], outputs:[{id:"meldScoreValue", label:"MELD Score"}], infoMessage:"MELD score calculation is complex. This provides an estimate. MELD-Na may also be used.", formulaText:"Logarithmic formula based on Cr, Bili, INR. See specific guidelines.", 
                    calculate: function(v){ let cr=parseFloat(v.creatinineMELD),bili=parseFloat(v.bilirubinMELD),inr=parseFloat(v.inrMELD); if(isNaN(cr)||isNaN(bili)||isNaN(inr))return{error:"Creatinine, Bilirubin, and INR are required."}; if(v.onDialysisMELD==="yes" || cr > 4.0) cr=4.0; else if(cr < 1.0 && (v.creatinineMELD && v.creatinineMELD !== '')) cr = Math.max(cr, 0.8); else if(cr<1.0) cr=1.0; /* Default if not provided or to avoid log issues */  if(bili<1.0)bili=1.0; if(inr<1.0)inr=1.0; let meld=Math.round((0.957*Math.log(cr)+0.378*Math.log(bili)+1.120*Math.log(inr)+0.643)*10); if(meld<6)meld=6; if(meld>40)meld=40; return {meldScoreValue:meld};}, 
                    getCalculationBreakdown: function(v,r){ return `Cr: ${v.creatinineMELD}, Bili: ${v.bilirubinMELD}, INR: ${v.inrMELD}, Dialysis: ${v.onDialysisMELD}.<br>Calculated MELD Score: <strong class="results-strong-text-color">${r.meldScoreValue}</strong>. (Sodium ${v.sodiumMELD || 'N/A'})`;}, 
                    interpretResult:function(r){ return `MELD Score: ${r.meldScoreValue}. Predicts 3-month mortality for end-stage liver disease and is used for liver transplant allocation. Higher scores indicate higher mortality risk and priority. Ranges 6-40.`;}}
            ]
        },
        {
            category: "Perioperative Medicine", categoryIcon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M14.121 14.121L19 19m-7-7l7-7m-7 7l-2.879 2.879M12 12L9.121 9.121m0 0L19 19" /></svg>`,
            calculators: [
                {id: "hasBledScore", name: "HAS-BLED Score",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 9,
                        ranges: [
                            { till: 2, label: 'Low-Mod. Risk', color: '#22c55e' },
                            { till: 9, label: 'High Risk', color: '#ef4444' }
                        ]
                    },
                    inputs: [
                        {id: "hypertensionHASBLED", label:"Hypertension (uncontrolled SBP >160)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "abnormalRenalHASBLED", label:"Abnormal Renal Function (dialysis, transplant, Cr>2.26)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "abnormalLiverHASBLED", label:"Abnormal Liver Function (cirrhosis, Bili>2xULN, AST/ALT/ALP>3xULN)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "strokeHASBLED", label:"Stroke History", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "bleedingHistoryHASBLED", label:"Bleeding History or Predisposition", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "labileINRSHASBLED", label:"Labile INRs (TTR <60%)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "elderlyHASBLED", label:"Elderly (Age > 65 years)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "drugsHASBLED", label:"Drugs (Antiplatelets, NSAIDs)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "alcoholHASBLED", label:"Alcohol (≥8 drinks/week)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                    ], outputs:[{id:"hasBledTotal", label:"HAS-BLED Score", unit: "/ 9"}], formulaText:"H(1) A(1or2) S(1) B(1) L(1) E(1) D(1or2). Sum points.", 
                    calculate: function(v){const s=parseInt(v.hypertensionHASBLED||0)+parseInt(v.abnormalRenalHASBLED||0)+parseInt(v.abnormalLiverHASBLED||0)+parseInt(v.strokeHASBLED||0)+parseInt(v.bleedingHistoryHASBLED||0)+parseInt(v.labileINRSHASBLED||0)+parseInt(v.elderlyHASBLED||0)+parseInt(v.drugsHASBLED||0)+parseInt(v.alcoholHASBLED||0); return{hasBledTotal:s};}, 
                    getCalculationBreakdown: function(v,r){return `HTN: ${v.hypertensionHASBLED||0}, Renal: ${v.abnormalRenalHASBLED||0}, Liver: ${v.abnormalLiverHASBLED||0}, Stroke: ${v.strokeHASBLED||0}, Bleed Hist: ${v.bleedingHistoryHASBLED||0}, INR: ${v.labileINRSHASBLED||0}, Age>65: ${v.elderlyHASBLED||0}, Drugs: ${v.drugsHASBLED||0}, Alcohol: ${v.alcoholHASBLED||0}.<br>Total = <strong class="results-strong-text-color">${r.hasBledTotal}</strong>`;}, 
                    interpretResult:function(r){ const s = r.hasBledTotal; if(s>=3) return "High risk of major bleeding (Score ≥3). This score identifies modifiable risk factors and encourages caution. It does not necessarily contraindicate anticoagulation but warrants close monitoring."; return "Low-moderate risk of major bleeding (Score 0-2).";}},
                {id: "leeScore", name: "Revised Cardiac Risk Index (RCRI / Lee Score)",
                    visualizationType: "donutChart",
                    visualizationParams: { 
                        unit: '',
                        maxScore: 6,
                        ranges: [
                            { till: 0, label: 'Class I (~0.4% risk)', color: '#22c55e' },
                            { till: 1, label: 'Class II (~0.9% risk)', color: '#f59e0b' },
                            { till: 2, label: 'Class III (~6.6% risk)', color: '#ef4444' },
                            { till: 6, label: 'Class IV (~11% risk)', color: '#a855f7' }
                        ]
                    },
                    inputs: [
                        {id: "highRiskSurgeryLee", label:"High-Risk Surgery (intraperitoneal, intrathoracic, suprainguinal vascular)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "ihdLee", label:"History of Ischemic Heart Disease (MI, +stress test, angina, nitrates)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "chfLee", label:"History of Congestive Heart Failure", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "cvdLee", label:"History of Cerebrovascular Disease (Stroke/TIA)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "insulinLee", label:"Preoperative Insulin Treatment for Diabetes", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                        {id: "creatinineLee", label:"Preoperative Serum Creatinine >2.0 mg/dL (>177 µmol/L)", type:"select", options:[{value:"0", text:"No (0)"},{value:"1", text:"Yes (1)"}]},
                    ], outputs:[{id:"leeTotal", label:"RCRI Score", unit: "/ 6"}, {id:"leeRiskClass", label:"Risk Class"}], formulaText:"Sum of 6 independent risk factors.", 
                    calculate: function(v){const s=parseInt(v.highRiskSurgeryLee||0)+parseInt(v.ihdLee||0)+parseInt(v.chfLee||0)+parseInt(v.cvdLee||0)+parseInt(v.insulinLee||0)+parseInt(v.creatinineLee||0); let rc=""; if(s===0)rc="Class I (Risk ~0.4%)"; else if(s===1)rc="Class II (Risk ~0.9%)"; else if(s===2)rc="Class III (Risk ~6.6%)"; else rc="Class IV (Risk ~11%)"; return{leeTotal:s, leeRiskClass:rc};}, 
                    getCalculationBreakdown: function(v,r){return `High-Risk Surg: ${v.highRiskSurgeryLee||0}, IHD: ${v.ihdLee||0}, CHF: ${v.chfLee||0}, CVD: ${v.cvdLee||0}, Insulin: ${v.insulinLee||0}, Cr>2: ${v.creatinineLee||0}.<br>Total = <strong class="results-strong-text-color">${r.leeTotal} (${r.leeRiskClass})</strong>`;}, 
                    interpretResult:function(r){return `Score: ${r.leeTotal}, ${r.leeRiskClass}. Predicts risk of major adverse cardiac events post-op. Higher classes may warrant further cardiac evaluation before non-cardiac surgery.`;}}
            ]
        }
    ];

    let currentCalculator = null;
    let dynamicListCounters = {}; 

    // DOM Elements
    const calculatorWidgetsHost = document.getElementById('calculatorWidgetsHost');
    const searchInput = document.getElementById('searchInput');
    const noResultsDiv = document.getElementById('no-results');
    
    // Modal DOM Elements
    const modal = document.getElementById('calculator-modal');
    const modalContentWrapper = document.getElementById('modal-content-wrapper');
    const modalTitle = document.getElementById('modal-title');
    const modalInputs = document.getElementById('modal-inputs');
    const modalResultCard = document.getElementById('modal-result-card');
    const modalCloseBtn = document.getElementById('modal-close-btn');
    const modalCalculateBtn = document.getElementById('modal-calculate-btn');
    const modalClearBtn = document.getElementById('modal-clear-btn');
    const calculatorForm = document.getElementById('calculator-form');

    function sanitizeHTML(str) {
        if (typeof str !== 'string') return String(str);
        const temp = document.createElement('div');
        temp.textContent = str;
        return temp.innerHTML;
    }

    function renderCalculatorWidgetsPage(filteredData = allCalculatorsData) {
        calculatorWidgetsHost.innerHTML = ''; 
        noResultsDiv.classList.toggle('hidden', filteredData.length > 0);

        let cardCounter = 0;
        filteredData.forEach(category => {
            const categorySection = document.createElement('section');
            categorySection.className = 'mb-12';

            const categoryTitleEl = document.createElement('h2');
            categoryTitleEl.className = 'text-2xl font-bold text-text-secondary mb-6 pb-2 border-b border-b-glass-border flex items-center gap-3';
            categoryTitleEl.innerHTML = `<span class="text-blue-400">${category.categoryIcon || ''}</span> ${category.category}`;
            categorySection.appendChild(categoryTitleEl);

            const widgetsGrid = document.createElement('div');
            widgetsGrid.className = 'grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-5 sm:gap-6';
            
            category.calculators.forEach(calc => {
                const isConverter = calc.widgetType && (calc.widgetType.startsWith('converter'));
                const cardElement = isConverter ? 'div' : 'button';
                const widget = document.createElement(cardElement);
                if (!isConverter) widget.type = 'button';
                
                widget.className = 'calculator-widget p-5 flex flex-col justify-start items-start text-left stagger-fade-in';
                widget.style.animationDelay = `${cardCounter * 50}ms`;
                if (!isConverter) {
                    widget.setAttribute('data-calculator-id', calc.id);
                    widget.setAttribute('aria-label', `Open ${calc.name} calculator`);
                    widget.onclick = () => setActiveCalculator(calc.id);
                }
                
                let innerHTML = `<h3 class="font-semibold text-lg text-text-primary leading-tight mb-1">${calc.name}</h3>`;
                
                if (!isConverter) {
                     innerHTML += `<p class="text-sm text-text-accent mt-1">${category.category}</p>`;
                } else {
                     innerHTML += renderConverterBody(calc);
                }

                widget.innerHTML = innerHTML;

                if (isConverter) {
                    addConverterEventListeners(widget, calc);
                }

                widgetsGrid.appendChild(widget);
                cardCounter++;
            });
            categorySection.appendChild(widgetsGrid);
            calculatorWidgetsHost.appendChild(categorySection);
        });
    }

    function renderConverterBody(calc) {
        let body = '<div class="w-full mt-3 space-y-3">';
        
        if (calc.widgetType === 'converter-special' && calc.id === 'heightConverter') {
            body += `
                <div class="flex items-center gap-2">
                    <div class="flex-1">
                        <label for="${calc.inputs[0].id}" class="block text-xs text-text-accent mb-1">${calc.inputs[0].unit}</label>
                        <input type="number" id="${calc.inputs[0].id}" data-calc-id="${calc.id}" class="input-glass w-full text-sm !py-2">
                    </div>
                </div>
                <div class="flex items-center gap-2">
                    <div class="flex-1">
                        <label for="${calc.inputs[1].id}" class="block text-xs text-text-accent mb-1">${calc.inputs[1].unit}</label>
                        <input type="number" id="${calc.inputs[1].id}" data-calc-id="${calc.id}" class="input-glass w-full text-sm !py-2">
                    </div>
                    <div class="flex-1">
                        <label for="${calc.inputs[2].id}" class="block text-xs text-text-accent mb-1">${calc.inputs[2].unit}</label>
                        <input type="number" id="${calc.inputs[2].id}" data-calc-id="${calc.id}" class="input-glass w-full text-sm !py-2">
                    </div>
                </div>
            `;
        } else {
            calc.inputs.forEach((input, index) => {
                body += `
                    <div>
                        <label for="${input.id}" class="block text-xs text-text-accent mb-1">${input.unit}</label>
                        <input type="number" step="any" id="${input.id}" data-calc-id="${calc.id}" class="input-glass w-full text-sm !py-2">
                    </div>
                `;
            });
        }
        
        body += '</div>';
        return body;
    }

    function addConverterEventListeners(widget, calc) {
        calc.inputs.forEach(inputDef => {
            const inputEl = widget.querySelector(`#${inputDef.id}`);
            if (inputEl) {
                inputEl.addEventListener('input', (e) => handleConverterChange(e, calc));
            }
        });
    }

    function handleConverterChange(event, calc) {
        const sourceInput = event.target;
        const sourceId = sourceInput.id;
        const sourceValue = parseFloat(sourceInput.value);

        // Clear other inputs if source is empty or invalid
        if (sourceInput.value.trim() === '' || isNaN(sourceValue)) {
            calc.inputs.forEach(inputDef => {
                if (inputDef.id !== sourceId) {
                    const targetInput = document.getElementById(inputDef.id);
                    if (targetInput) targetInput.value = '';
                }
            });
            return;
        }

        let allValues = {};
        if (calc.widgetType === 'converter-special') {
             calc.inputs.forEach(inputDef => {
                 const el = document.getElementById(inputDef.id);
                 if(el) allValues[inputDef.id] = el.value;
             });
        }

        const result = calc.calculate({ value: sourceValue, sourceId: sourceId, allValues: allValues });

        for (const targetId in result) {
            const targetInput = document.getElementById(targetId);
            if (targetInput) {
                const resValue = result[targetId];
                if (!isNaN(parseFloat(resValue))) {
                     // Avoid tiny floating point inaccuracies
                    targetInput.value = Number(parseFloat(resValue).toPrecision(6));
                } else {
                    targetInput.value = '';
                }
            }
        }
    }
    
    function setActiveCalculator(calculatorId) {
        const calculator = allCalculatorsData.flatMap(cat => cat.calculators).find(c => c.id === calculatorId);
        if (!calculator) return;

        currentCalculator = calculator;
        renderCalculatorUI(calculator);

        modal.classList.remove('hidden');
        modal.classList.add('flex');
        document.body.style.overflow = 'hidden';

        setTimeout(() => {
            modalContentWrapper.classList.add('scale-100', 'opacity-100');
            modalContentWrapper.classList.remove('scale-95', 'opacity-0');
        }, 10);
    }
    
    function closeModal() {
        modalContentWrapper.classList.remove('scale-100', 'opacity-100');
        modalContentWrapper.classList.add('scale-95', 'opacity-0');
        setTimeout(() => {
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            document.body.style.overflow = '';
            currentCalculator = null;
        }, 300);
    }

    function createInputField(inputDef) {
        const formGroupId = `form-group-${inputDef.id}`;
        let existingGroup = document.getElementById(formGroupId);
        if (existingGroup) {
            existingGroup.innerHTML = '';
        } else {
            existingGroup = document.createElement('div');
            existingGroup.id = formGroupId;
        }
        
        const isDynamicList = inputDef.type === 'dynamicList';
        existingGroup.className = isDynamicList ? 'md:col-span-2 mb-2' : 'mb-2';

        const label = document.createElement('label');
        label.htmlFor = inputDef.id;
        label.className = 'block text-sm font-medium mb-1.5';
        label.textContent = inputDef.label + (inputDef.unit ? ` (${inputDef.unit})` : '');
        existingGroup.appendChild(label);

        if (inputDef.type === 'select') {
            const select = document.createElement('select');
            select.id = inputDef.id;
            select.name = inputDef.id;
            select.className = 'input-glass w-full';
            (inputDef.options || []).forEach(opt => {
                const option = document.createElement('option');
                option.value = opt.value;
                option.textContent = opt.text;
                select.appendChild(option);
            });
            existingGroup.appendChild(select);
        } else if (isDynamicList) {
            const listContainerId = `${inputDef.id}-list`;
            dynamicListCounters[inputDef.id] = 0;

            const listDiv = document.createElement('div');
            listDiv.id = listContainerId;
            listDiv.className = 'space-y-3 mt-1';
            existingGroup.appendChild(listDiv);

            const addButton = document.createElement('button');
            addButton.type = 'button';
            addButton.textContent = `+ Add ${inputDef.listName} Item`;
            addButton.className = 'mt-2 text-sm py-1.5 px-3 bg-blue-600/50 hover:bg-blue-600/70 text-white rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-slate-800 focus:ring-blue-500 transition-all';
            addButton.onclick = () => addDynamicListItem(inputDef.id, listContainerId);
            existingGroup.appendChild(addButton);

        } else {
            const input = document.createElement('input');
            input.type = inputDef.type;
            input.id = inputDef.id;
            input.name = inputDef.id;
            input.className = 'input-glass w-full';
            if (inputDef.placeholder) input.placeholder = inputDef.placeholder;
            if (inputDef.type === "number") {
                 input.step = "any";
                 input.oninput = (e) => e.target.classList.remove('input-error-border');
            }
            if(inputDef.type === 'date') {
                input.classList.add('appearance-none'); 
            }
            existingGroup.appendChild(input);
        }
        const errorSpanId = `${inputDef.id}-error`;
        const errorSpan = document.createElement('span');
        errorSpan.id = errorSpanId;
        errorSpan.className = 'input-error-message hidden mt-1'; 
        errorSpan.setAttribute('aria-live', 'assertive');
        existingGroup.appendChild(errorSpan);

        return existingGroup;
    }

    function addDynamicListItem(listBaseId, containerId) {
        const listContainer = document.getElementById(containerId);
        const itemId = dynamicListCounters[listBaseId]++;
        
        const itemDiv = document.createElement('div');
        itemDiv.className = 'flex items-center space-x-2 p-2.5 border border-glass-border rounded-lg bg-slate-900/50';
        itemDiv.id = `${listBaseId}-item-${itemId}`;

        const descInput = document.createElement('input');
        descInput.type = 'text';
        descInput.name = `${listBaseId}_description_${itemId}`;
        descInput.placeholder = 'Item Description (e.g., Oral)';
        descInput.className = 'flex-grow input-glass !py-1.5';
        
        const amountInput = document.createElement('input');
        amountInput.type = 'number';
        amountInput.name = `${listBaseId}_amount_${itemId}`;
        amountInput.placeholder = 'Amount (mL)';
        amountInput.step = "any";
        amountInput.className = 'w-32 input-glass !py-1.5';
        amountInput.oninput = (e) => {
            if (parseFloat(e.target.value) < 0) e.target.classList.add('input-error-border');
            else e.target.classList.remove('input-error-border');
        };

        const removeButton = document.createElement('button');
        removeButton.type = 'button';
        removeButton.innerHTML = '&times;'; 
        removeButton.setAttribute('aria-label', 'Remove item');
        removeButton.className = 'py-1 px-2.5 bg-red-600/50 hover:bg-red-600/80 text-white rounded-md text-xs font-bold focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-slate-800 focus:ring-red-500 transition-all';
        removeButton.onclick = () => itemDiv.remove();

        itemDiv.appendChild(descInput);
        itemDiv.appendChild(amountInput);
        itemDiv.appendChild(removeButton);
        listContainer.appendChild(itemDiv);
        descInput.focus();
    }

    function renderCalculatorUI(calculator) {
        modalTitle.textContent = calculator.name;
        modalInputs.innerHTML = '';
        modalResultCard.innerHTML = '';
        modalResultCard.classList.add('hidden');
        calculatorForm.reset();
        
        (calculator.inputs || []).forEach(inputDef => {
            modalInputs.appendChild(createInputField(inputDef));
        });
    }
    
    function clearErrorMessages() {
        document.querySelectorAll(`#calculator-form .input-error-message`).forEach(span => {
            span.textContent = '';
            span.classList.add('hidden');
        });
        document.querySelectorAll(`#calculator-form .input-error-border`).forEach(el => {
            el.classList.remove('input-error-border');
        });
    }

    function displayErrorMessage(inputFieldId, message) {
        const errorSpan = document.getElementById(`${inputFieldId}-error`);
        const inputEl = document.getElementById(inputFieldId);
        if (errorSpan) {
            errorSpan.textContent = message;
            errorSpan.classList.remove('hidden');
        }
        if (inputEl) {
             inputEl.classList.add('input-error-border');
             if(document.activeElement !== inputEl) inputEl.focus();
        }
    }
    
    // --- VISUALIZATION FUNCTIONS ---

    function createDonutChart(score, params) {
        const { unit = '', maxScore, ranges } = params;
        const container = document.createElement('div');
        container.className = 'visualization-container my-4';

        const size = 160;
        const strokeWidth = 12;
        const radius = (size / 2) - (strokeWidth * 2);
        const circumference = 2 * Math.PI * radius;
        const offset = circumference - (score / maxScore) * circumference;

        const range = ranges.find(r => score <= r.till) || ranges[ranges.length - 1];
        const color = range.color;
        const label = range.label;

        const svgHTML = `
            <svg class="w-full h-auto" viewBox="0 0 ${size} ${size}">
                <circle class="donut-chart-track" stroke-width="${strokeWidth}" fill="transparent" r="${radius}" cx="${size/2}" cy="${size/2}" />
                <circle class="donut-chart-value" stroke="${color}" stroke-width="${strokeWidth}" fill="transparent" r="${radius}" cx="${size/2}" cy="${size/2}"
                        style="stroke-dasharray: ${circumference}; stroke-dashoffset: ${circumference}; transform: rotate(-90deg); transform-origin: 50% 50%;" />
                <text x="50%" y="48%" dominant-baseline="middle" text-anchor="middle" class="fill-current text-text-primary" font-size="28" font-weight="bold">
                    ${score}<tspan font-size="16" class="fill-current text-text-accent">${unit ? ' ' + unit : `/${maxScore}`}</tspan>
                </text>
                <text x="50%" y="65%" dominant-baseline="middle" text-anchor="middle" class="fill-current" font-size="12" style="fill: ${color};" font-weight="600">
                    ${label}
                </text>
            </svg>
        `;

        container.innerHTML = svgHTML;
        setTimeout(() => {
            const circle = container.querySelector('.donut-chart-value');
            if (circle) circle.style.strokeDashoffset = offset;
        }, 100);

        return container;
    }

    function createLinearGauge(value, params) {
        const { unit = '', ranges, displayMin, displayMax } = params;
        const container = document.createElement('div');
        container.className = 'visualization-container my-4 py-2';
        
        const totalRange = displayMax - displayMin;
        const valuePercent = ((value - displayMin) / totalRange) * 100;
        const range = ranges.find(r => value < r.max) || ranges[ranges.length - 1];
        const label = range.label;
        const color = range.color;

        let lastStop = displayMin;
        const rangeSegments = ranges.map(r => {
            const width = ((r.max - lastStop) / totalRange) * 100;
            lastStop = r.max;
            return `<div class="h-full" style="width: ${width}%; background-color: ${r.color};"></div>`;
        }).join('');

        const gaugeHTML = `
            <div class="relative w-full">
                <div class="absolute -top-7 text-center transition-all" style="left: ${valuePercent}%;">
                    <div class="text-sm font-bold" style="color: ${color};">${value} ${unit}</div>
                    <div class="w-0 h-0 border-l-4 border-l-transparent border-r-4 border-r-transparent border-t-4 mx-auto" style="border-top-color: ${color};"></div>
                </div>
                <div class="h-2.5 w-full linear-gauge-track rounded-full flex overflow-hidden">${rangeSegments}</div>
                <div class="flex justify-between text-xs text-text-accent mt-1.5">
                    <span>${displayMin}</span>
                    <span>${displayMax}</span>
                </div>
            </div>
        `;
        container.innerHTML = gaugeHTML;
        return container;
    }

    function createBarChart(data) {
        const intake = data.totalIntake;
        const output = data.totalOutput;
        const balance = data.finalBalance;

        const container = document.createElement('div');
        container.className = 'visualization-container my-4';

        const maxVal = Math.max(intake, output, 100); // ensure a minimum height
        const intakeHeight = (intake / maxVal) * 100;
        const outputHeight = (output / maxVal) * 100;
        const balanceColor = balance >= 0 ? 'text-green-400' : 'text-red-400';
        const balanceSign = balance >= 0 ? '+' : '';

        const chartHTML = `
            <div class="relative h-48 w-full">
                <!-- Grid lines -->
                <div class="absolute top-0 left-0 w-full h-full">
                    <div class="h-1/4 w-full border-b border-dashed border-white/10"></div>
                    <div class="h-1/4 w-full border-b border-dashed border-white/10"></div>
                    <div class="h-1/4 w-full border-b border-dashed border-white/10"></div>
                    <div class="h-1/4 w-full"></div>
                </div>
                <!-- Bars -->
                <div class="absolute bottom-0 left-0 right-0 flex justify-around items-end h-full px-4">
                    <div class="w-1/3 text-center">
                        <div class="font-bold text-sm text-blue-300">${intake} mL</div>
                        <div class="bar-chart-bar w-1/2 mx-auto bg-blue-500 rounded-t-md" style="height: 0%;"></div>
                        <div class="text-xs font-semibold text-text-secondary mt-1">Intake</div>
                    </div>
                     <div class="w-1/3 text-center">
                        <div class="font-bold text-sm text-red-300">${output} mL</div>
                        <div class="bar-chart-bar w-1/2 mx-auto bg-red-500 rounded-t-md" style="height: 0%;"></div>
                        <div class="text-xs font-semibold text-text-secondary mt-1">Output</div>
                    </div>
                </div>
            </div>
            <div class="text-center mt-4">
                <div class="text-sm text-text-accent">Fluid Balance</div>
                <div class="text-2xl font-bold ${balanceColor}">${balanceSign}${balance} mL</div>
            </div>
        `;

        container.innerHTML = chartHTML;
        setTimeout(() => {
            const bars = container.querySelectorAll('.bar-chart-bar');
            bars[0].style.height = `${intakeHeight}%`;
            bars[1].style.height = `${outputHeight}%`;
        }, 100);

        return container;
    }


    function handleCalculate(calculator) {
        const formData = new FormData(calculatorForm);
        const values = {};
        let firstErrorFieldId = null;
        let hasError = false;

        clearErrorMessages();

        for (const inputDef of (calculator.inputs || [])) {
            if (inputDef.type === 'dynamicList') {
                values[inputDef.id] = [];
                const listContainer = document.getElementById(`${inputDef.id}-list`);
                if (listContainer) {
                    const items = listContainer.querySelectorAll(':scope > div'); 
                    items.forEach((itemDiv, index) => {
                        const descInput = itemDiv.querySelector('input[type="text"]');
                        const amountInput = itemDiv.querySelector('input[type="number"]');
                        const description = descInput ? descInput.value.trim() : `Item ${index + 1}`;
                        const amountStr = amountInput ? amountInput.value : ''; 
                        
                        if (amountStr.trim() === '' || isNaN(parseFloat(amountStr)) || parseFloat(amountStr) < 0) {
                            if (amountInput) amountInput.classList.add('input-error-border');
                            hasError = true;
                            if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                        } else {
                            if (amountInput) amountInput.classList.remove('input-error-border');
                        }
                        values[inputDef.id].push({ description, amount: amountStr });
                    });
                     if (calculator.id === 'fluidBalance' && hasError && firstErrorFieldId === inputDef.id) {
                         displayErrorMessage(inputDef.id, 'One or more amounts in the list are invalid, empty, or negative.');
                    }
                }
            } else {
                const value = formData.get(inputDef.id);
                values[inputDef.id] = value; 
                 if (inputDef.unit) values[`${inputDef.id}_unit`] = inputDef.unit;

                if (!value && inputDef.type !== 'select' && inputDef.type !== 'dynamicList' && inputDef.type !== 'text' && (calculator.inputs || []).find(i => i.id === inputDef.id)) { 
                    displayErrorMessage(inputDef.id, 'This field is required.');
                    if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                    hasError = true;
                } else if (inputDef.type === 'number' && value && (isNaN(parseFloat(value)) || !isFinite(value) )) {
                     displayErrorMessage(inputDef.id, 'Please enter a valid number.');
                     if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                     hasError = true;
                } else if (inputDef.type === 'date' && value) {
                    const today = new Date(); today.setHours(0,0,0,0);
                    const selectedDate = new Date(value + "T00:00:00");
                    if (calculator.id === 'eddNaegeles' && selectedDate > today) {
                        displayErrorMessage(inputDef.id, 'LMP date cannot be in the future.');
                        if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                        hasError = true;
                    }
                }
                if (inputDef.type === 'number' && value && parseFloat(value) < 0) {
                    const generallyPositiveIds = ['desiredDose', 'doseOnHand', 'volumeVehicle', 'totalVolume', 'totalTimeHours', 'totalVolumeGtt', 'totalTimeMinutes', 'dropFactor', 'weightKg', 'heightCm', 'ageYearsCG', 'weightCrClCG', 'serumCreatinineCG', 'prescribedDosePerKg', 'weightPeds', 'dosesPerDay', 'weightFluidsPeds', 'weightUrinePeds', 'shiftDuration', 'sbpMap', 'dbpMap', 'weightBurn', 'tbsa', 'mapForCpp', 'pao2'];
                     const nonNegativeIds = ['icp'];
                     if (generallyPositiveIds.includes(inputDef.id)) {
                        displayErrorMessage(inputDef.id, 'Value must be positive.');
                        if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                        hasError = true;
                     } else if (nonNegativeIds.includes(inputDef.id) && parseFloat(value) < 0) {
                        displayErrorMessage(inputDef.id, 'Value must be non-negative.');
                        if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                        hasError = true;
                     }
                }
                if (inputDef.id === 'fio2' && value && (parseFloat(value) < 21 || parseFloat(value) > 100)) {
                    displayErrorMessage(inputDef.id, 'FiO2 must be between 21% and 100%.');
                    if(!firstErrorFieldId) firstErrorFieldId = inputDef.id;
                    hasError = true;
                }
            }
        }
        
        if (hasError) return;

        const resultData = calculator.calculate(values);
        modalResultCard.innerHTML = ''; 

        if (resultData.error) {
            modalResultCard.innerHTML = `<p class="mt-4 p-3 bg-red-500/30 text-red-300 border border-red-500/50 rounded-lg text-sm">${resultData.error}</p>`;
        } else {
            const resultCard = document.createElement('div');
            resultCard.className = 'results-card-bg'; 

            const patientIconDiv = document.createElement('div');
            patientIconDiv.className = 'flex items-center mb-4';
            patientIconDiv.innerHTML = `
                <svg class="patient-icon" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" /></svg>
                <h3 class="text-xl font-semibold text-text-primary">${calculator.name} Results</h3>
            `;
            resultCard.appendChild(patientIconDiv);

            if(resultData.info && calculator.infoMessage) {
                 resultCard.innerHTML += `<p class="mt-4 p-3 bg-blue-500/20 text-blue-200 border border-blue-500/30 rounded-lg text-sm">${sanitizeHTML(calculator.infoMessage)}</p>`;
            }

            if (calculator.visualizationType && !resultData.info) {
                let vizElement = null;
                const vizParams = calculator.visualizationParams;

                if (calculator.visualizationType === 'donutChart' && vizParams) {
                    const score = parseFloat(resultData[calculator.outputs[0].id]);
                    vizElement = createDonutChart(score, vizParams);
                } else if (calculator.visualizationType === 'linearGauge' && vizParams) {
                    const value = parseFloat(resultData[calculator.outputs[0].id]);
                    vizElement = createLinearGauge(value, vizParams);
                } else if (calculator.visualizationType === 'barChart') {
                    vizElement = createBarChart(resultData);
                }
                if(vizElement) resultCard.appendChild(vizElement);
            }

            if(calculator.outputs && calculator.outputs.length > 0 && calculator.visualizationType !== 'barChart') {
                const outputsContainer = document.createElement('div');
                outputsContainer.className = 'grid grid-cols-1 sm:grid-cols-2 gap-4 mt-4';
                calculator.outputs.forEach(outputDef => {
                    if (resultData[outputDef.id] !== undefined) {
                        const outputDiv = document.createElement('div');
                        outputDiv.className = 'bg-slate-900/50 p-3 rounded-lg text-center';
                        outputDiv.innerHTML = `
                            <div class="text-sm text-text-accent">${outputDef.label}</div>
                            <div class="text-xl font-bold results-strong-text-color">${sanitizeHTML(String(resultData[outputDef.id]))} ${outputDef.unit || ''}</div>
                        `;
                        outputsContainer.appendChild(outputDiv);
                    }
                });
                resultCard.appendChild(outputsContainer);
            }
            
            const interpretation = calculator.interpretResult && !resultData.info ? calculator.interpretResult(resultData, values) : null;
            if (interpretation) {
                resultCard.innerHTML += `
                    <h4 class="text-md font-semibold text-text-accent mt-5 mb-2">Interpretation:</h4>
                    <p class="text-sm font-medium interpretation-bg p-3 rounded-lg">${sanitizeHTML(interpretation)}</p>`;
            }

            if (calculator.getCalculationBreakdown && !resultData.info) {
                resultCard.innerHTML += `
                    <details class="mt-4">
                        <summary class="text-md font-semibold text-text-accent cursor-pointer">Calculation Breakdown</summary>
                        <div class="mt-2 text-sm space-y-1 breakdown-bg p-3 rounded-lg border border-glass-border">
                           ${calculator.getCalculationBreakdown(values, resultData)}
                        </div>
                    </details>`;
            }
            
            modalResultCard.appendChild(resultCard);
        }
        modalResultCard.classList.remove('hidden');
        modalResultCard.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function handleSearch() {
        const searchTerm = searchInput.value.toLowerCase().trim();
        if (!searchTerm) {
            renderCalculatorWidgetsPage(allCalculatorsData);
            return;
        }
        const trulyFiltered = [];
        allCalculatorsData.forEach(category => {
            const categoryNameLower = category.category.toLowerCase();
            let calculatorsForThisCategory = category.calculators.filter(calc =>
                calc.name.toLowerCase().includes(searchTerm)
            );

            if (calculatorsForThisCategory.length > 0) {
                 if (!trulyFiltered.find(c => c.category === category.category)) {
                    trulyFiltered.push({ ...category, calculators: calculatorsForThisCategory });
                 }
            }
        });
        renderCalculatorWidgetsPage(trulyFiltered);
    }
    
    document.addEventListener('DOMContentLoaded', () => {
        renderCalculatorWidgetsPage();

        searchInput.addEventListener('input', handleSearch);
        
        // Modal listeners
        modalCloseBtn.addEventListener('click', closeModal);
        modal.addEventListener('click', (e) => {
            if (e.target === modal) closeModal();
        });
        
        modalCalculateBtn.addEventListener('click', (e) => {
            e.preventDefault();
            if (currentCalculator) handleCalculate(currentCalculator);
        });

        modalClearBtn.addEventListener('click', () => {
            if(currentCalculator) renderCalculatorUI(currentCalculator);
        });

        calculatorForm.addEventListener('submit', (e) => {
            e.preventDefault();
            if (currentCalculator) handleCalculate(currentCalculator);
        });
    });
</script>
</body>
</html>
