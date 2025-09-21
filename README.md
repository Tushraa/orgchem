<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AlChem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0d1117;
            color: white;
            overflow-x: hidden;
        }
        .bg-lines-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            overflow: hidden;
        }
        .content-container {
            position: relative;
            z-index: 1;
        }
        .logo-container {
            background-color: #0b0e14;
            border: 2px solid rgba(255, 255, 255, 0.2);
            padding: 0.5rem;
            border-radius: 0.5rem;
            box-shadow: 0 0 10px rgba(0, 255, 255, 0.3);
        }
        .tab-content {
            display: none;
            width: 100%;
            max-width: 100%;
            margin-left: auto;
            margin-right: auto;
            align-items: center;
            justify-content: center;
        }
        .tab-content.active {
            display: flex;
        }
    </style>
</head>
<body class="bg-[#0d1117]">

    <div class="bg-lines-container">
        <canvas id="lineCanvas" class="w-full h-full"></canvas>
    </div>

    <!-- Main Content -->
    <div class="content-container flex flex-col min-h-screen p-4 md:p-8">
        <!-- Header -->
        <header class="w-full bg-[#0b0e14] bg-opacity-80 backdrop-blur-sm shadow-lg py-4 px-8 md:px-16 flex justify-between items-center z-20 rounded-xl">
            <div class="flex items-center space-x-2">
                <div class="logo-container hidden md:block">
                    <svg class="h-6 w-6 text-cyan-400" viewBox="0 0 24 24" fill="currentColor" stroke="none">
                        <path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zM12 4.5a7.5 7.5 0 0 1 7.5 7.5 7.5 7.5 0 0 1-7.5 7.5A7.5 7.5 0 0 1 4.5 12 7.5 7.5 0 0 1 12 4.5zM12 6a6 6 0 0 0-5.196 9A6 6 0 0 0 12 18a6 6 0 0 0 5.196-9A6 6 0 0 0 12 6zM12 8a4 4 0 0 0-3.464 6A4 4 0 0 0 12 16a4 4 0 0 0 3.464-6A4 4 0 0 0 12 8zM12 10a2 2 0 1 0 0 4 2 2 0 0 0 0-4z"/>
                    </svg>
                </div>
                <span class="text-xl font-bold text-white">AlChem</span>
            </div>
            <nav class="hidden md:flex space-x-8 text-sm font-medium">
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="explainer">Chemistry Explainer</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="calculators">Calculators</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="asap-articles">ASAP Articles</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="bioisosteres">Bioisosteres</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="spirocycles">Spirocycles</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="total-synthesis">Total Synthesis</button>
            </nav>
            <button id="mobileMenuButton" class="md:hidden text-white focus:outline-none">
                <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
                </svg>
            </button>
        </header>

        <!-- Mobile Menu -->
        <div id="mobileMenu" class="md:hidden fixed top-0 left-0 w-full h-full bg-[#0d1117] bg-opacity-95 z-40 transition-transform transform -translate-x-full">
            <div class="flex justify-end p-8">
                <button id="closeMenuButton" class="text-white focus:outline-none">
                    <svg class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                    </svg>
                </button>
            </div>
            <nav class="flex flex-col items-center space-y-8 text-xl font-medium">
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="explainer">Chemistry Explainer</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="calculators">Calculators</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="asap-articles">ASAP Articles</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="bioisosteres">Bioisosteres</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="spirocycles">Spirocycles</button>
                <button class="tab-button hover:text-cyan-400 transition-colors" data-tab="total-synthesis">Total Synthesis</button>
            </nav>
        </div>

        <main class="flex-grow flex flex-col items-center justify-center p-4">

            <!-- Tab Content Containers -->
            <div id="explainer" class="tab-content active p-6 md:p-16 w-full flex-grow flex items-center justify-center">
                <div class="bg-gray-800 bg-opacity-50 backdrop-blur-sm p-6 rounded-xl shadow-lg w-full max-w-2xl border border-gray-700">
                    <h2 class="text-2xl font-bold mb-4 text-cyan-300">Chemistry Explainer ✨</h2>
                    <p class="text-gray-300 mb-4">Enter a chemistry concept below to get a simple, concise explanation.</p>
                    <textarea id="conceptInput" rows="4" placeholder="e.g., What is a covalent bond?" class="w-full bg-gray-900 border border-gray-700 text-white rounded-lg p-3 focus:outline-none focus:border-cyan-400 mb-4"></textarea>
                    <button id="explainButton" class="w-full bg-cyan-600 hover:bg-cyan-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors focus:outline-none focus:ring-2 focus:ring-cyan-500 focus:ring-offset-2 focus:ring-offset-gray-900">
                        Explain Chemistry Concept ✨
                    </button>
                    <div id="loadingIndicator" class="mt-4 hidden text-center text-cyan-300">
                        <p>Generating explanation...</p>
                    </div>
                    <div id="explanationOutput" class="mt-4 p-4 bg-gray-900 rounded-lg border border-gray-700">
                        <p class="text-gray-400">Your explanation will appear here.</p>
                    </div>
                    <div id="sourcesOutput" class="mt-2 text-xs text-gray-500"></div>
                </div>
            </div>

            <div id="calculators" class="tab-content p-6 md:p-16 w-full flex-grow flex items-center justify-center">
                <div class="bg-gray-800 bg-opacity-50 backdrop-blur-sm p-6 rounded-xl shadow-lg w-full max-w-2xl border border-gray-700">
                    <h2 class="text-2xl font-bold mb-4 text-cyan-300">Chemistry Calculators 🧪</h2>
                    
                    <h3 class="text-xl font-bold mt-4 text-white">Molecular Weight & Exact Mass</h3>
                    <p class="text-gray-300 mb-4">Enter a chemical formula (e.g., $C_6H_{12}O_6$) to calculate its molecular and exact mass.</p>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-gray-400 mb-1">Chemical Formula</label>
                            <input id="formulaInput" type="text" class="w-full bg-gray-900 border border-gray-700 text-white rounded-lg p-3 focus:outline-none focus:border-cyan-400" placeholder="e.g., C6H12O6">
                        </div>
                    </div>
                    <button id="calculateFormula" class="w-full mt-6 bg-cyan-600 hover:bg-cyan-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors focus:outline-none focus:ring-2 focus:ring-cyan-500 focus:ring-offset-2 focus:ring-offset-gray-900">Calculate</button>
                    <div id="formulaResult" class="mt-4 p-4 bg-gray-900 rounded-lg border border-gray-700 text-gray-400">Result:</div>

                    <h3 class="text-xl font-bold mt-8 text-white">Molarity Calculator</h3>
                    <p class="text-gray-300 mb-4">Calculate the molarity of a solution.</p>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-gray-400 mb-1">Moles of Solute (mol)</label>
                            <input id="molarityMoles" type="number" step="any" class="w-full bg-gray-900 border border-gray-700 text-white rounded-lg p-3 focus:outline-none focus:border-cyan-400">
                        </div>
                        <div>
                            <label class="block text-gray-400 mb-1">Volume of Solution (L)</label>
                            <input id="molarityVolume" type="number" step="any" class="w-full bg-gray-900 border border-gray-700 text-white rounded-lg p-3 focus:outline-none focus:border-cyan-400">
                        </div>
                    </div>
                    <button id="calculateMolarity" class="w-full mt-6 bg-cyan-600 hover:bg-cyan-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors focus:outline-none focus:ring-2 focus:ring-cyan-500 focus:ring-offset-2 focus:ring-offset-gray-900">Calculate Molarity</button>
                    <div id="molarityResult" class="mt-4 p-4 bg-gray-900 rounded-lg border border-gray-700 text-gray-400">Result:</div>

                    <h3 class="text-xl font-bold mt-8 text-white">Normality Calculator</h3>
                    <p class="text-gray-300 mb-4">Calculate the normality of a solution.</p>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-gray-400 mb-1">Gram Equivalent Weight</label>
                            <input id="normalityGEW" type="number" step="any" class="w-full bg-gray-900 border border-gray-700 text-white rounded-lg p-3 focus:outline-none focus:border-cyan-400">
                        </div>
                        <div>
                            <label class="block text-gray-400 mb-1">Volume of Solution (L)</label>
                            <input id="normalityVolume" type="number" step="any" class="w-full bg-gray-900 border border-gray-700 text-white rounded-lg p-3 focus:outline-none focus:border-cyan-400">
                        </div>
                    </div>
                    <button id="calculateNormality" class="w-full mt-6 bg-cyan-600 hover:bg-cyan-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors focus:outline-none focus:ring-2 focus:ring-cyan-500 focus:ring-offset-2 focus:ring-offset-gray-900">Calculate Normality</button>
                    <div id="normalityResult" class="mt-4 p-4 bg-gray-900 rounded-lg border border-gray-700 text-gray-400">Result:</div>
                </div>
            </div>

            <div id="asap-articles" class="tab-content p-6 md:p-16 w-full flex-grow flex items-center justify-center">
                <div class="bg-gray-800 bg-opacity-50 backdrop-blur-sm p-6 rounded-xl shadow-lg w-full max-w-2xl border border-gray-700">
                    <h2 class="text-2xl font-bold mb-4 text-cyan-300">ASAP Articles 📰</h2>
                    <p class="text-gray-300 mb-4">Get a summary of recent ASAP (As Soon As Publishable) articles. </p>
                    <button id="fetchArticlesBtn" class="w-full bg-cyan-600 hover:bg-cyan-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors focus:outline-none focus:ring-2 focus:ring-cyan-500 focus:ring-offset-2 focus:ring-offset-gray-900">Fetch Latest Articles</button>
                    <div id="asapLoading" class="mt-4 hidden text-center text-cyan-300">
                        <p>Fetching articles...</p>
                    </div>
                    <div id="articlesOutput" class="mt-4 space-y-8"></div>
                </div>
            </div>

            <div id="bioisosteres" class="tab-content p-6 md:p-16 w-full flex-grow flex items-center justify-center">
                <div class="bg-gray-800 bg-opacity-50 backdrop-blur-sm p-6 rounded-xl shadow-lg w-full max-w-2xl border border-gray-700">
                    <h2 class="text-2xl font-bold mb-4 text-cyan-300">Bioisosteres 🔗</h2>
                    <div id="bioisosteresContent" class="text-gray-300">
                        <div id="bioisosteresLoading" class="mt-4 text-center text-cyan-300">
                            <p>Loading explanation...</p>
                        </div>
                    </div>
                </div>
            </div>

            <div id="spirocycles" class="tab-content p-6 md:p-16 w-full flex-grow flex items-center justify-center">
                <div class="bg-gray-800 bg-opacity-50 backdrop-blur-sm p-6 rounded-xl shadow-lg w-full max-w-2xl border border-gray-700">
                    <h2 class="text-2xl font-bold mb-4 text-cyan-300">Spirocycles 🌀</h2>
                    <div id="spirocyclesContent" class="text-gray-300">
                        <div id="spirocyclesLoading" class="mt-4 text-center text-cyan-300">
                            <p>Loading explanation...</p>
                        </div>
                    </div>
                </div>
            </div>

            <div id="total-synthesis" class="tab-content p-6 md:p-16 w-full flex-grow flex items-center justify-center">
                <div class="bg-gray-800 bg-opacity-50 backdrop-blur-sm p-6 rounded-xl shadow-lg w-full max-w-2xl border border-gray-700">
                    <h2 class="text-2xl font-bold mb-4 text-cyan-300">Total Synthesis ⚛️</h2>
                    <div id="totalSynthesisContent" class="text-gray-300">
                        <div id="totalSynthesisLoading" class="mt-4 text-center text-cyan-300">
                            <p>Loading explanation...</p>
                        </div>
                    </div>
                </div>
            </div>

        </main>

        <!-- Footer -->
        <footer class="w-full text-center py-4 text-gray-500 text-sm mt-8">
            <p>&copy; 2024 AlChem. All rights reserved.</p>
        </footer>
    </div>

    <script>
        // --- Canvas Animation ---
        const canvas = document.getElementById('lineCanvas');
        const ctx = canvas.getContext('2d');
        const dpr = window.devicePixelRatio || 1;

        let lines = [];
        let points = [];
        const numLines = 5;
        const numPoints = 10;

        function resizeCanvas() {
            canvas.width = window.innerWidth * dpr;
            canvas.height = window.innerHeight * dpr;
            ctx.scale(dpr, dpr);
            lines = [];
            points = [];
            createLines();
            createPoints();
        }

        function createLines() {
            for (let i = 0; i < numLines; i++) {
                const startX = (i + 1) * (canvas.width / (numLines + 1));
                const endX = startX - (Math.random() * 200 + 100);
                lines.push({ startX, startY: 0, endX, endY: canvas.height });
            }
        }

        function createPoints() {
            for (let i = 0; i < numPoints; i++) {
                const lineIndex = Math.floor(Math.random() * lines.length);
                const line = lines[lineIndex];
                points.push({
                    lineIndex,
                    progress: Math.random(),
                    size: Math.random() * 2 + 1,
                    speed: Math.random() * 0.005 + 0.002
                });
            }
        }

        function drawLines() {
            ctx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
            ctx.lineWidth = 2;
            ctx.lineCap = 'round';
            lines.forEach(line => {
                ctx.beginPath();
                ctx.moveTo(line.startX, line.startY);
                ctx.lineTo(line.endX, line.endY);
                ctx.stroke();
            });
        }

        function drawPoints() {
            points.forEach(point => {
                const line = lines[point.lineIndex];
                const x = line.startX + (line.endX - line.startX) * point.progress;
                const y = line.startY + (line.endY - line.startY) * point.progress;
                ctx.fillStyle = 'white';
                ctx.beginPath();
                ctx.arc(x, y, point.size, 0, Math.PI * 2);
                ctx.fill();
            });
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawLines();
            drawPoints();
            points.forEach(point => {
                point.progress += point.speed;
                if (point.progress > 1) {
                    point.progress = 0;
                    point.lineIndex = Math.floor(Math.random() * lines.length);
                }
            });
            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', resizeCanvas);
        window.onload = () => {
            resizeCanvas();
            animate();
            showTab('explainer');
            fetchInfo('bioisosteres');
            fetchInfo('spirocycles');
            fetchInfo('total-synthesis');
        };

        // --- Mobile Menu ---
        const mobileMenuButton = document.getElementById('mobileMenuButton');
        const mobileMenu = document.getElementById('mobileMenu');
        const closeMenuButton = document.getElementById('closeMenuButton');

        mobileMenuButton.addEventListener('click', () => {
            mobileMenu.classList.remove('-translate-x-full');
            mobileMenu.classList.add('translate-x-0');
        });

        closeMenuButton.addEventListener('click', () => {
            mobileMenu.classList.remove('translate-x-0');
            mobileMenu.classList.add('-translate-x-full');
        });

        // --- Tab Switching Logic ---
        const tabs = document.querySelectorAll('.tab-button');
        const tabContents = document.querySelectorAll('.tab-content');

        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                const targetTab = tab.getAttribute('data-tab');
                showTab(targetTab);
                if (mobileMenu.classList.contains('translate-x-0')) {
                    mobileMenu.classList.remove('translate-x-0');
                    mobileMenu.classList.add('-translate-x-full');
                }
            });
        });

        function showTab(tabId) {
            tabContents.forEach(content => {
                content.classList.remove('active');
            });
            document.getElementById(tabId).classList.add('active');
        }

        // --- Gemini API Call Wrapper ---
        async function callGeminiApi(payload, loadingId, outputId) {
            const loadingIndicator = document.getElementById(loadingId);
            const outputDiv = document.getElementById(outputId);
            loadingIndicator.classList.remove('hidden');
            
            const apiKey = "";
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;

            let response;
            let retries = 0;
            const maxRetries = 3;

            while (retries < maxRetries) {
                try {
                    response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (response.status !== 429) break;
                    await new Promise(resolve => setTimeout(resolve, Math.pow(2, retries) * 1000));
                    retries++;
                } catch (error) {
                    console.error("Fetch failed, retrying...", error);
                    await new Promise(resolve => setTimeout(resolve, Math.pow(2, retries) * 1000));
                    retries++;
                }
            }
            loadingIndicator.classList.add('hidden');

            if (!response || !response.ok) {
                outputDiv.innerHTML = `<p class="text-red-400">Error: Could not connect to the API.</p>`;
                throw new Error(`API call failed with status: ${response ? response.status : 'No response'}`);
            }

            const result = await response.json();
            const candidate = result.candidates?.[0];
            if (!candidate || !candidate.content?.parts?.[0]) {
                outputDiv.innerHTML = `<p class="text-red-400">Error: No content was generated.</p>`;
                throw new Error("No content generated from API.");
            }

            return candidate;
        }

        // --- Tab 1: Chemistry Explainer ---
        const conceptInput = document.getElementById('conceptInput');
        const explainButton = document.getElementById('explainButton');
        const loadingIndicator = document.getElementById('loadingIndicator');
        const explanationOutput = document.getElementById('explanationOutput');
        const sourcesOutput = document.getElementById('sourcesOutput');

        explainButton.addEventListener('click', async () => {
            const concept = conceptInput.value.trim();
            if (!concept) {
                explanationOutput.innerHTML = '<p class="text-red-400">Please enter a chemistry concept to explain.</p>';
                return;
            }

            explainButton.disabled = true;
            try {
                const systemPrompt = "You are a friendly and knowledgeable chemistry tutor. Explain the provided chemistry concept concisely and in simple terms, suitable for a high school student.";
                const userQuery = `Explain: ${concept}`;
                const payload = {
                    contents: [{ parts: [{ text: userQuery }] }],
                    tools: [{ "google_search": {} }],
                    systemInstruction: {
                        parts: [{ text: systemPrompt }]
                    },
                };
                const candidate = await callGeminiApi(payload, 'loadingIndicator', 'explanationOutput');
                
                explanationOutput.innerHTML = `<p>${candidate.content.parts[0].text}</p>`;
                
                const groundingMetadata = candidate.groundingMetadata;
                if (groundingMetadata && groundingMetadata.groundingAttributions) {
                    const sources = groundingMetadata.groundingAttributions
                        .map(attribution => ({ uri: attribution.web?.uri, title: attribution.web?.title }))
                        .filter(source => source.uri && source.title);
                    if (sources.length > 0) {
                        let sourcesHtml = '<p>Sources:</p><ul>';
                        sources.forEach(source => { sourcesHtml += `<li><a href="${source.uri}" target="_blank" class="text-cyan-400 hover:underline">${source.title}</a></li>`; });
                        sourcesHtml += '</ul>';
                        sourcesOutput.innerHTML = sourcesHtml;
                    }
                }
            } catch (error) {
                console.error("Error in explainer:", error);
                explanationOutput.innerHTML = `<p class="text-red-400">An error occurred while generating the explanation.</p>`;
            } finally {
                explainButton.disabled = false;
            }
        });

        // --- Tab 2: Calculators ---
        const molarityBtn = document.getElementById('calculateMolarity');
        const normalityBtn = document.getElementById('calculateNormality');
        const molecularWeightBtn = document.getElementById('calculateFormula');

        // Molarity Calculator
        molarityBtn.addEventListener('click', () => {
            const moles = parseFloat(document.getElementById('molarityMoles').value);
            const volume = parseFloat(document.getElementById('molarityVolume').value);
            const resultDiv = document.getElementById('molarityResult');
            if (isNaN(moles) || isNaN(volume) || volume <= 0) {
                resultDiv.innerHTML = 'Result: Invalid input.';
                return;
            }
            const molarity = moles / volume;
            resultDiv.innerHTML = `Result: ${molarity.toFixed(4)} M`;
        });

        // Normality Calculator
        normalityBtn.addEventListener('click', () => {
            const gew = parseFloat(document.getElementById('normalityGEW').value);
            const volume = parseFloat(document.getElementById('normalityVolume').value);
            const resultDiv = document.getElementById('normalityResult');
            if (isNaN(gew) || isNaN(volume) || volume <= 0) {
                resultDiv.innerHTML = 'Result: Invalid input.';
                return;
            }
            const normality = gew / volume;
            resultDiv.innerHTML = `Result: ${normality.toFixed(4)} N`;
        });

        // Molecular Weight & Exact Mass Calculator
        const exactAtomicWeights = {
            'H': 1.00782503223, 'He': 4.00260325413, 'Li': 7.01600455, 'Be': 9.0121822, 'B': 11.0093054,
            'C': 12.0000000, 'N': 14.00307400443, 'O': 15.99491461957, 'F': 18.9984031627, 'Ne': 19.9924401754,
            'Na': 22.989769282, 'Mg': 23.985041700, 'Al': 26.9815385, 'Si': 27.9769265325, 'P': 30.973761998,
            'S': 31.97207117, 'Cl': 34.96885268, 'K': 39.0987114, 'Ar': 39.9623831237, 'Ca': 39.96259086,
            'Fe': 55.9349375, 'Cu': 62.9295977, 'Ag': 106.905097, 'Au': 196.966570, 'Pb': 203.9730436, 'Hg': 201.970643, 'Zn': 63.9291422
        };

        const standardAtomicWeights = {
            'H': 1.008, 'He': 4.003, 'Li': 6.941, 'Be': 9.012, 'B': 10.811, 'C': 12.011, 'N': 14.007, 'O': 15.999,
            'F': 18.998, 'Ne': 20.180, 'Na': 22.990, 'Mg': 24.305, 'Al': 26.982, 'Si': 28.085, 'P': 30.974,
            'S': 32.065, 'Cl': 35.453, 'K': 39.098, 'Ar': 39.948, 'Ca': 40.078, 'Fe': 55.845, 'Cu': 63.546,
            'Ag': 107.868, 'Au': 196.967, 'Pb': 207.2, 'Hg': 200.592, 'Zn': 65.38
        };

        molecularWeightBtn.addEventListener('click', () => {
            const formula = document.getElementById('formulaInput').value.trim();
            const resultDiv = document.getElementById('formulaResult');
            if (!formula) {
                resultDiv.innerHTML = 'Result: Please enter a chemical formula.';
                return;
            }

            let totalMolecularWeight = 0;
            let totalExactMass = 0;
            let currentElement = '';
            let currentCount = '';

            for (let i = 0; i < formula.length; i++) {
                const char = formula[i];
                if (char >= 'A' && char <= 'Z') {
                    if (currentElement) {
                        const count = currentCount === '' ? 1 : parseInt(currentCount);
                        const molWeight = standardAtomicWeights[currentElement];
                        const exactMass = exactAtomicWeights[currentElement];
                        if (molWeight === undefined || exactMass === undefined) {
                            resultDiv.innerHTML = `Result: Unknown element '${currentElement}'.`;
                            return;
                        }
                        totalMolecularWeight += molWeight * count;
                        totalExactMass += exactMass * count;
                    }
                    currentElement = char;
                    currentCount = '';
                } else if (char >= 'a' && char <= 'z') {
                    currentElement += char;
                } else if (char >= '0' && char <= '9') {
                    currentCount += char;
                }
            }

            if (currentElement) {
                const count = currentCount === '' ? 1 : parseInt(currentCount);
                const molWeight = standardAtomicWeights[currentElement];
                const exactMass = exactAtomicWeights[currentElement];
                if (molWeight === undefined || exactMass === undefined) {
                    resultDiv.innerHTML = `Result: Unknown element '${currentElement}'.`;
                    return;
                }
                totalMolecularWeight += molWeight * count;
                totalExactMass += exactMass * count;
            }

            resultDiv.innerHTML = `Result:<br>Molecular Weight: ${totalMolecularWeight.toFixed(4)} g/mol<br>Exact Mass: ${totalExactMass.toFixed(8)} amu`;
        });

        // --- Tab 3: ASAP Articles ---
        const fetchArticlesBtn = document.getElementById('fetchArticlesBtn');
        const articlesOutput = document.getElementById('articlesOutput');

        fetchArticlesBtn.addEventListener('click', async () => {
            articlesOutput.innerHTML = '';
            try {
                const systemPrompt = "You are a research assistant tasked with summarizing key information from recent chemistry articles. Focus on articles from journals like J. Org. Chem., J. Am. Chem. Soc., or Angewandte Chemie. Extract the title, authors, a concise summary of the abstract (2-3 sentences max), the journal name, and the URL. Format the output as a JSON array of objects.";
                const userQuery = "Find 5 recent ASAP (As Soon As Publishable) articles in organic chemistry.";
                
                const payload = {
                    contents: [{ parts: [{ text: userQuery }] }],
                    tools: [{ "google_search": {} }],
                    systemInstruction: { parts: [{ text: systemPrompt }] },
                    generationConfig: {
                        responseMimeType: "application/json",
                        responseSchema: {
                            type: "ARRAY",
                            items: {
                                type: "OBJECT",
                                properties: {
                                    "title": { "type": "STRING" },
                                    "authors": { "type": "STRING" },
                                    "abstract_summary": { "type": "STRING" },
                                    "journal": { "type": "STRING" },
                                    "link": { "type": "STRING" }
                                },
                                "propertyOrdering": ["title", "authors", "abstract_summary", "journal", "link"]
                            }
                        }
                    }
                };

                const candidate = await callGeminiApi(payload, 'asapLoading', 'articlesOutput');
                
                const articles = JSON.parse(candidate.content.parts[0].text);
                if (articles.length === 0) {
                    articlesOutput.innerHTML = `<p class="text-red-400">No articles found. Please try again later.</p>`;
                    return;
                }

                articles.forEach(article => {
                    const articleHtml = `
                        <div class="bg-gray-700 p-4 rounded-lg">
                            <h3 class="text-xl font-semibold text-cyan-200 mb-2">${article.title}</h3>
                            <p class="text-gray-400 text-sm mb-2"><strong>Authors:</strong> ${article.authors}</p>
                            <p class="text-gray-300 mb-2">${article.abstract_summary}</p>
                            <a href="${article.link}" target="_blank" class="text-cyan-400 hover:underline">Read full article in ${article.journal}</a>
                        </div>
                    `;
                    articlesOutput.innerHTML += articleHtml;
                });

            } catch (error) {
                console.error("Error fetching articles:", error);
                articlesOutput.innerHTML = `<p class="text-red-400">An error occurred while fetching articles.</p>`;
            }
        });

        // --- Tabs 4-6: Bioisosteres, Spirocycles, Total Synthesis ---
        const topics = {
            'bioisosteres': 'Bioisosteres',
            'spirocycles': 'Spirocycles',
            'total-synthesis': 'Total Synthesis'
        };

        async function fetchInfo(tabId) {
            const outputDiv = document.getElementById(`${tabId}Content`);
            const loadingDiv = document.getElementById(`${tabId}Loading`);

            if(outputDiv.innerHTML.trim() !== `<div id="${tabId}Loading" class="mt-4 text-center text-cyan-300">
                            <p>Loading explanation...</p>
                        </div>`) {
                return;
            }

            loadingDiv.classList.remove('hidden');
            
            try {
                const topic = topics[tabId];
                const systemPrompt = "You are an expert organic chemistry writer. Provide a detailed, easy-to-understand explanation of the provided topic.";
                const userQuery = `Explain the organic chemistry concept of ${topic}.`;

                const payload = {
                    contents: [{ parts: [{ text: userQuery }] }],
                    tools: [{ "google_search": {} }],
                    systemInstruction: { parts: [{ text: systemPrompt }] },
                };

                const candidate = await callGeminiApi(payload, `${tabId}Loading`, `${tabId}Content`);
                
                outputDiv.innerHTML = `
                    <p class="text-gray-300">${candidate.content.parts[0].text}</p>
                    <div id="${tabId}Sources" class="mt-4 text-xs text-gray-500"></div>
                `;

                const groundingMetadata = candidate.groundingMetadata;
                if (groundingMetadata && groundingMetadata.groundingAttributions) {
                    const sources = groundingMetadata.groundingAttributions
                        .map(attribution => ({ uri: attribution.web?.uri, title: attribution.web?.title }))
                        .filter(source => source.uri && source.title);
                    if (sources.length > 0) {
                        let sourcesHtml = '<p>Sources:</p><ul>';
                        sources.forEach(source => { sourcesHtml += `<li><a href="${source.uri}" target="_blank" class="text-cyan-400 hover:underline">${source.title}</a></li>`; });
                        sourcesHtml += '</ul>';
                        document.getElementById(`${tabId}Sources`).innerHTML = sourcesHtml;
                    }
                }
            } catch (error) {
                console.error(`Error fetching ${tabId} info:`, error);
                outputDiv.innerHTML = `<p class="text-red-400">An error occurred while fetching the information.</p>`;
            } finally {
                loadingDiv.classList.add('hidden');
            }
        }
    </script>
</body>
</html>

