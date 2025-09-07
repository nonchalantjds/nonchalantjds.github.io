<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Case for China's Solar Energy Development</title>
    <script src="https://cdn.tailwindcss.com?plugins=typography"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: "Warm Neutral" - A calming and professional palette using beige, slate, soft gold, and deep green for accents. -->
    <!-- Application Structure Plan: The application is designed as a single-page, vertically scrolling interactive report, mirroring the structure of a debate presentation. The user flows from a high-level introduction to detailed sections covering the current situation, future potential, technology, and challenges. This thematic, linear structure is chosen for its clarity and ease of use in debate preparation, allowing a user to build their argument step-by-step. Interactive charts provide data-driven evidence, and toggleable sections for 'Challenges' allow for quick preparation of rebuttals, making it a highly effective study tool. -->
    <!-- Visualization & Content Choices: 
        1. Installed Capacity Growth: Goal=Show change/scale. Viz=Bar Chart (Chart.js). Interaction=Tooltips on hover. Justification=Effectively demonstrates the exponential growth narrative.
        2. Energy Mix Share: Goal=Show proportion. Viz=Donut Chart (Chart.js). Interaction=Tooltips on hover. Justification=Clearly communicates solar's rising importance in the overall energy landscape.
        3. Key Statistics: Goal=Inform/Impact. Viz=Dynamic Counters (HTML/JS). Interaction=Numbers animate on scroll. Justification=Provides quick, memorable, high-impact data points.
        4. Tech Developments: Goal=Organize/Inform. Viz=Interactive Cards (HTML/JS). Interaction=Click to reveal details. Justification=Presents complex information in a digestible, user-controlled format.
        5. Problems & Rebuttals: Goal=Compare/Analyze. Viz=Toggleable Content Blocks (HTML/JS). Interaction=Click to reveal affirmative counter-argument. Justification=Directly prepares user for debate by framing challenges and providing sophisticated rebuttals.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFBF8; /* Warm Beige */
            color: #334155; /* Cool Slate */
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #B48A3D; /* Soft Gold */
            border-bottom-color: #B48A3D;
        }
        .chart-container {
            position: relative; 
            width: 100%; 
            max-width: 700px; 
            margin-left: auto; 
            margin-right: auto; 
            height: 350px; 
            max-height: 45vh;
        }
        @media (min-width: 768px) { 
            .chart-container { 
                height: 450px; 
            } 
        }
        .stat-card {
            background-color: #FFFFFF;
            border: 1px solid #E2E8F0;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        .tech-card {
            cursor: pointer;
            transition: all 0.3s;
        }
        .tech-card .details {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out;
        }
        .tech-card.open .details {
            max-height: 500px; /* Adjust as needed */
            transition: max-height 0.7s ease-in;
        }
        .gemini-btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            transition: all 0.3s;
        }
        .gemini-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        .loader {
            display: none;
        }
        .loader.active {
            display: flex;
        }
    </style>
</head>
<body class="antialiased">

    <!-- Header & Navigation -->
    <header class="bg-white/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <h1 class="text-xl font-bold text-[#2C5F2D]">Affirmative Case: China's Solar Dominance</h1>
            <div class="hidden md:flex space-x-8">
                <a href="#intro" class="nav-link font-medium">Introduction</a>
                <a href="#current" class="nav-link font-medium">Current Situation</a>
                <a href="#potential" class="nav-link font-medium">Potential</a>
                <a href="#tech" class="nav-link font-medium">Technology</a>
                <a href="#rebuttals" class="nav-link font-medium">Rebuttals</a>
                <a href="#conclusion" class="nav-link font-medium">Conclusion</a>
            </div>
            <div class="md:hidden">
                <select id="mobile-nav" class="bg-gray-200 border border-gray-300 rounded-md p-2">
                    <option value="#intro">Introduction</option>
                    <option value="#current">Current Situation</option>
                    <option value="#potential">Potential</option>
                    <option value="#tech">Technology</option>
                    <option value="#rebuttals">Rebuttals</option>
                    <option value="#conclusion">Conclusion</option>
                </select>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-6 py-12">

        <!-- Section 1: Introduction -->
        <section id="intro" class="text-center py-16">
            <h2 class="text-4xl md:text-5xl font-extrabold text-[#2C5F2D] mb-4">Forging a Green Future</h2>
            <p class="max-w-3xl mx-auto text-lg text-slate-600">
                China's development of solar energy is not merely an industrial strategy; it is a decisive, large-scale transformation that positions the nation as the undisputed global leader in renewable technology. This commitment provides a powerful blueprint for global decarbonization, enhances energy security, and fuels sustainable economic growth. We stand in firm support of the continued and accelerated development of solar energy in China as a critical necessity for both national prosperity and planetary health.
            </p>
        </section>

        <!-- Section 2: Current Situation -->
        <section id="current" class="py-16">
            <div class="text-center mb-12">
                <h3 class="text-3xl font-bold text-slate-800">An Unprecedented Scale of Deployment</h3>
                <p class="mt-2 text-md text-slate-500 max-w-2xl mx-auto">China's solar capacity has grown exponentially, outpacing the rest of the world combined. This section visualizes the sheer magnitude of this achievement and its tangible impact on the energy landscape. The data clearly shows a nation not just adopting solar, but leading a global energy revolution from the front.</p>
            </div>
            <div class="grid md:grid-cols-3 gap-8 mb-12">
                <div class="stat-card rounded-xl p-6 text-center shadow-lg">
                    <p class="text-5xl font-bold text-[#B48A3D]" id="capacity-stat">0</p>
                    <p class="text-slate-600 mt-2 font-medium">Gigawatts of Installed Solar Capacity (2025)</p>
                </div>
                <div class="stat-card rounded-xl p-6 text-center shadow-lg">
                    <p class="text-5xl font-bold text-[#B48A3D]" id="global-share-stat">0</p>
                    <p class="text-slate-600 mt-2 font-medium">% Share of Global Solar Panel Manufacturing</p>
                </div>
                 <div class="stat-card rounded-xl p-6 text-center shadow-lg">
                    <p class="text-5xl font-bold text-[#B48A3D]" id="investment-stat">0</p>
                    <p class="text-slate-600 mt-2 font-medium">Trillion Yuan Clean Energy Investment (2024)</p>
                </div>
            </div>
            <div class="grid lg:grid-cols-5 gap-8 items-center">
                <div class="lg:col-span-3 bg-white p-6 rounded-xl shadow-lg">
                    <h4 class="text-xl font-semibold text-center mb-4">Explosive Growth in Solar Capacity (GW)</h4>
                    <div class="chart-container">
                        <canvas id="capacityChart"></canvas>
                    </div>
                </div>
                <div class="lg:col-span-2 bg-white p-6 rounded-xl shadow-lg">
                    <h4 class="text-xl font-semibold text-center mb-4">Renewable Energy Mix (2025)</h4>
                     <div class="chart-container" style="height: 400px; max-height:40vh;">
                        <canvas id="mixChart"></canvas>
                    </div>
                </div>
            </div>
             <!-- Gemini API Feature: Latest News -->
            <div class="mt-12 bg-slate-50 p-6 rounded-xl shadow-inner">
                <h4 class="text-xl font-semibold text-center mb-4 text-[#2C5F2D]">Get the Latest News & Analysis</h4>
                <p class="text-center text-slate-600 mb-6 max-w-2xl mx-auto">Click the button below to get a real-time summary of the most recent developments in China's solar industry, powered by the Gemini API with Google Search.</p>
                <div class="text-center">
                    <button id="getNewsBtn" class="gemini-btn bg-[#B48A3D] text-white font-bold py-2 px-6 rounded-lg hover:bg-[#a37a30]">
                        <span>✨</span> Fetch Latest Intel
                    </button>
                </div>
                <div id="newsResult" class="mt-6 hidden">
                    <div id="newsLoader" class="loader justify-center items-center">
                        <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-[#B48A3D]"></div>
                    </div>
                    <div id="newsContent" class="prose max-w-none text-slate-700 bg-white p-4 rounded-md"></div>
                    <div id="newsSources" class="mt-4 hidden">
                        <h5 class="font-semibold text-slate-800">Sources:</h5>
                        <ul class="list-disc list-inside text-sm text-slate-600 space-y-1"></ul>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 3: Potential for Further Exploitation -->
        <section id="potential" class="py-16 bg-white rounded-xl shadow-lg">
            <div class="text-center mb-12 px-4">
                <h3 class="text-3xl font-bold text-slate-800">The Horizon of Opportunity is Vast</h3>
                <p class="mt-2 text-md text-slate-500 max-w-2xl mx-auto">Despite record-breaking achievements, China has only begun to tap into its immense solar potential. This section explores the strategic drivers—government ambition, economic incentives, and vast geographical resources—that ensure solar development will continue its aggressive upward trajectory, securing future energy independence and economic leadership.</p>
            </div>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8 px-6">
                <div class="p-6 bg-slate-50 rounded-lg potential-point">
                    <h4 class="text-xl font-semibold text-[#2C5F2D] mb-2">Ambitious National Targets</h4>
                    <p class="text-slate-600">The upcoming 15th Five-Year Plan (2026-2030) is projected to mandate an annual increase of 200-300 GW in renewable capacity. China has already surpassed its 2030 renewable targets six years ahead of schedule, demonstrating a pattern of under-promising and over-delivering.</p>
                </div>
                <div class="p-6 bg-slate-50 rounded-lg potential-point">
                    <h4 class="text-xl font-semibold text-[#2C5F2D] mb-2">Economic Powerhouse</h4>
                    <p class="text-slate-600">Clean energy sectors contributed a record 13.6 trillion yuan ($1.9tn) to China's economy in 2024, driving a quarter of its GDP growth. Solar is a primary engine of this growth, creating jobs, attracting investment, and generating significant export revenue.</p>
                </div>
                <div class="p-6 bg-slate-50 rounded-lg potential-point">
                    <h4 class="text-xl font-semibold text-[#2C5F2D] mb-2">Vast Land & Resources</h4>
                    <p class="text-slate-600">Expansive deserts in western and northern China, like the Gobi Desert, offer unparalleled land availability for massive utility-scale solar farms. This geographical advantage allows for projects on a scale unimaginable in many other nations, with clear potential for further expansion.</p>
                </div>
                <div class="p-6 bg-slate-50 rounded-lg potential-point">
                    <h4 class="text-xl font-semibold text-[#2C5F2D] mb-2">Energy Security Imperative</h4>
                    <p class="text-slate-600">Reducing reliance on volatile foreign fossil fuel markets is a core strategic goal. Every gigawatt of solar installed domestically strengthens China's energy independence and insulates its economy from geopolitical shocks.</p>
                </div>
                 <div class="p-6 bg-slate-50 rounded-lg potential-point">
                    <h4 class="text-xl font-semibold text-[#2C5F2D] mb-2">Decentralized Energy Growth</h4>
                    <p class="text-slate-600">Beyond massive solar farms, there is enormous potential in distributed solar—rooftop panels on residential, commercial, and industrial buildings. This "solar everywhere" approach enhances grid resilience and empowers local communities.</p>
                </div>
                 <div class="p-6 bg-slate-50 rounded-lg potential-point">
                    <h4 class="text-xl font-semibold text-[#2C5F2D] mb-2">Global Market Leadership</h4>
                    <p class="text-slate-600">By continuing to scale up domestic deployment, China drives down global costs, making solar energy more affordable for all nations. This solidifies its role as an indispensable leader in the global energy transition.</p>
                </div>
            </div>
            <!-- Gemini API Feature: Generate Talking Points -->
            <div class="mt-8 pt-8 border-t border-slate-200 px-6">
                <h4 class="text-xl font-semibold text-center mb-4 text-[#2C5F2D]">Brainstorm More Arguments</h4>
                <p class="text-center text-slate-600 mb-6 max-w-2xl mx-auto">Need more firepower for your debate? Use the Gemini API to generate additional talking points based on the arguments above.</p>
                <div class="text-center">
                    <button id="getPointsBtn" class="gemini-btn bg-[#2C5F2D] text-white font-bold py-2 px-6 rounded-lg hover:bg-[#3A7D44]">
                        <span>✨</span> Generate New Talking Points
                    </button>
                </div>
                <div id="pointsResult" class="mt-6 hidden">
                    <div id="pointsLoader" class="loader justify-center items-center">
                         <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-[#2C5F2D]"></div>
                    </div>
                    <div id="pointsContent" class="prose max-w-none text-slate-700 bg-slate-50 p-4 rounded-md"></div>
                </div>
            </div>
        </section>

        <!-- Section 4: Current Technological Developments -->
        <section id="tech" class="py-16">
             <div class="text-center mb-12">
                <h3 class="text-3xl font-bold text-slate-800">Innovation at the Forefront</h3>
                <p class="mt-2 text-md text-slate-500 max-w-2xl mx-auto">China is not just the world's leading manufacturer of solar panels; it is a hub of technological innovation, pushing the boundaries of efficiency, applicability, and sustainability. This section highlights key advancements that are redefining what solar power can achieve. Click on each card to learn more.</p>
            </div>
            <div class="space-y-4">
                <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-[#B48A3D]">N-Type TOPCon & HJT Cells</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p>China's industry is rapidly shifting from older P-type PERC cells to next-generation N-type technologies like TOPCon (Tunnel Oxide Passivated Contact) and HJT (Heterojunction). These cells offer higher conversion efficiencies (exceeding 25-26%), lower degradation rates over time, and better performance in low-light conditions, resulting in significantly more energy yield over the panel's lifespan.</p>
                    </div>
                </div>
                <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-[#B48A3D]">Perovskite Tandem Cells</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p>A breakthrough technology where a layer of perovskite material is placed on top of a traditional silicon cell. This "tandem" structure captures a wider spectrum of light, dramatically boosting potential efficiency. Chinese labs and companies have set world records for this technology, with efficiencies exceeding 33%, promising a future of hyper-efficient panels.</p>
                    </div>
                </div>
                <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-[#B48A3D]">Bifacial Module Technology</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p>Bifacial panels can capture sunlight on both sides. By absorbing reflected light (albedo) from the ground or roof surface, they can generate up to 25% more electricity than their monofacial counterparts. Chinese manufacturers have perfected this technology, making it a standard for utility-scale and commercial projects.</p>
                    </div>
                </div>
                <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-[#B48A3D]">Agrivoltaics & Floating Solar</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p>China leads in innovative deployment methods that maximize land and water use. Agrivoltaics integrates solar panels with agriculture, providing shade for crops while generating power. Floating solar farms, built on reservoirs and lakes, conserve valuable land, reduce evaporation, and improve panel efficiency due to the cooling effect of water.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 5: Perceived Problems and Limitations (Rebuttals) -->
        <section id="rebuttals" class="py-16">
            <div class="text-center mb-12">
                <h3 class="text-3xl font-bold text-slate-800">Addressing the Challenges Head-On</h3>
                <p class="mt-2 text-md text-slate-500 max-w-2xl mx-auto">A robust argument acknowledges and refutes its weaknesses. While the scale of China's solar expansion presents challenges, they are not roadblocks but catalysts for further innovation. This section tackles potential criticisms with strong, evidence-based counterarguments, turning perceived limitations into points of strength.</p>
            </div>
            <div class="space-y-4">
                <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-red-700">Argument Against: "Solar energy is intermittent and unreliable, destabilizing the grid."</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p class="font-semibold text-green-700">Our Rebuttal:</p>
                        <p>This view is outdated. China is aggressively tackling intermittency by becoming a world leader in both energy storage and smart grid technology. Massive investments in battery storage facilities, pumped hydro, and the development of ultra-high-voltage (UHV) transmission lines are key parts of the strategy. UHV lines can transmit power from sun-rich western regions to eastern population centers with minimal loss, balancing supply and demand across the country. Solar is being integrated as part of a sophisticated, modern energy system, not as an isolated variable.</p>
                    </div>
                </div>
                <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-red-700">Argument Against: "China's dominance creates a risky global over-reliance on a single supply chain."</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p class="font-semibold text-green-700">Our Rebuttal:</p>
                        <p>China's industrial scale has been the single most important factor in making solar power the cheapest form of electricity in history, benefiting the entire world. This leadership was earned through strategic investment and innovation, not happenstance. While supply chain diversification is a valid global goal, penalizing China's success would slow the global energy transition and raise costs for everyone. Furthermore, China is now exporting not just panels, but also the cells, wafers, and manufacturing expertise that allow other countries like India, Türkiye, and Indonesia to build their own panel assembly industries, thereby fostering a more distributed global supply chain.</p>
                    </div>
                </div>
                 <div class="tech-card bg-white rounded-lg shadow p-6" onclick="toggleDetails(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="text-xl font-semibold text-red-700">Argument Against: "The land use for massive solar farms is environmentally destructive."</h4>
                        <span class="text-2xl font-thin transform transition-transform duration-300">+</span>
                    </div>
                    <div class="details pt-4 text-slate-600">
                        <p class="font-semibold text-green-700">Our Rebuttal:</p>
                        <p>This is a mischaracterization. The majority of China's large-scale solar projects are built on arid or degraded land in deserts, which have minimal agricultural or ecological value. In fact, projects like the massive solar park in the Kubuqi Desert have shown that the panels can reduce ground-level wind speeds and water evaporation, aiding in desert greening and combating desertification. When combined with innovative approaches like agrivoltaics and floating solar, the development of solar energy represents an efficient and often ecologically beneficial use of land and resources compared to any form of fossil fuel extraction.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 6: Conclusion -->
        <section id="conclusion" class="text-center py-16 bg-gradient-to-r from-[#2C5F2D] to-[#3A7D44] text-white rounded-lg">
            <h2 class="text-4xl font-extrabold mb-4">An Indisputable Engine for Progress</h2>
            <p class="max-w-3xl mx-auto text-lg text-gray-200">
                The evidence is overwhelming. China's pursuit of solar energy development is a resounding success story with profound positive implications. It is driving economic growth, creating technological leadership, enhancing national energy security, and making the single largest contribution of any nation to the global fight against climate change. The challenges that exist are being met with innovation and strategic planning. Therefore, we assert that the continued, robust development of solar energy in China is not just a wise policy, but an essential one for a sustainable and prosperous future.
            </p>
        </section>

    </main>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const API_KEY = ""; 
            const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${API_KEY}`;
            
            // Gemini API call function
            async function callGemini(prompt, useSearchGrounding = false) {
                const payload = {
                    contents: [{ parts: [{ text: prompt }] }],
                };

                if (useSearchGrounding) {
                    payload.tools = [{ "google_search": {} }];
                }

                try {
                    const response = await fetch(API_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        throw new Error(`API call failed with status: ${response.status}`);
                    }
                    return await response.json();
                } catch (error) {
                    console.error("Gemini API call error:", error);
                    return { error: "Failed to fetch data from the API. Please check the console for details." };
                }
            }
            
            // Get News Feature
            const getNewsBtn = document.getElementById('getNewsBtn');
            const newsResultDiv = document.getElementById('newsResult');
            const newsLoader = document.getElementById('newsLoader');
            const newsContentDiv = document.getElementById('newsContent');
            const newsSourcesDiv = document.getElementById('newsSources');
            const newsSourcesList = newsSourcesDiv.querySelector('ul');

            getNewsBtn.addEventListener('click', async () => {
                getNewsBtn.disabled = true;
                newsResultDiv.style.display = 'block';
                newsLoader.classList.add('active');
                newsContentDiv.innerHTML = '';
                newsSourcesDiv.style.display = 'none';
                newsSourcesList.innerHTML = '';

                const prompt = "In a concise summary, what are the latest news, statistics, and policy updates regarding China's solar energy development in 2025? Focus on information from the last 3-6 months. Present the key findings as a few clear bullet points in markdown format.";
                const result = await callGemini(prompt, true);
                
                newsLoader.classList.remove('active');

                if (result.error) {
                    newsContentDiv.innerHTML = `<p class="text-red-600">${result.error}</p>`;
                } else {
                    const candidate = result.candidates?.[0];
                    const text = candidate?.content?.parts?.[0]?.text || "No content returned.";
                    newsContentDiv.innerHTML = text.replace(/\*/g, '•');

                    const groundingMetadata = candidate?.groundingMetadata;
                    if (groundingMetadata?.groundingAttributions) {
                        const sources = groundingMetadata.groundingAttributions
                            .map(attr => ({ uri: attr.web?.uri, title: attr.web?.title }))
                            .filter(s => s.uri && s.title);
                        
                        if(sources.length > 0) {
                            sources.forEach(source => {
                                const li = document.createElement('li');
                                li.innerHTML = `<a href="${source.uri}" target="_blank" class="text-blue-600 hover:underline">${source.title}</a>`;
                                newsSourcesList.appendChild(li);
                            });
                            newsSourcesDiv.style.display = 'block';
                        }
                    }
                }
                getNewsBtn.disabled = false;
            });

            // Get Talking Points Feature
            const getPointsBtn = document.getElementById('getPointsBtn');
            const pointsResultDiv = document.getElementById('pointsResult');
            const pointsLoader = document.getElementById('pointsLoader');
            const pointsContentDiv = document.getElementById('pointsContent');

            getPointsBtn.addEventListener('click', async () => {
                getPointsBtn.disabled = true;
                pointsResultDiv.style.display = 'block';
                pointsLoader.classList.add('active');
                pointsContentDiv.innerHTML = '';

                const existingPoints = Array.from(document.querySelectorAll('.potential-point h4')).map(h4 => h4.textContent.trim()).join(', ');
                const prompt = `You are a world-class debate coach. Based on these existing arguments for China's solar potential: "${existingPoints}", generate three new, distinct, and compelling talking points. Each point should have a clear title (as a markdown heading) and a short, powerful explanation. Do not repeat the existing points.`;
                
                const result = await callGemini(prompt, false);

                pointsLoader.classList.remove('active');

                if (result.error) {
                    pointsContentDiv.innerHTML = `<p class="text-red-600">${result.error}</p>`;
                } else {
                    const text = result.candidates?.[0]?.content?.parts?.[0]?.text || "No new points generated.";
                    pointsContentDiv.innerHTML = text.replace(/###\s/g, '<h4 class="text-lg font-semibold text-[#2C5F2D] mt-4 mb-1">').replace(/\*\*/g, '');
                }
                getPointsBtn.disabled = false;
            });


            // Animate stats on scroll
            const animateValue = (obj, start, end, duration) => {
                let startTimestamp = null;
                const step = (timestamp) => {
                    if (!startTimestamp) startTimestamp = timestamp;
                    const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                    const currentValue = Math.floor(progress * (end - start) + start);
                    obj.innerHTML = currentValue.toLocaleString();
                    if (progress < 1) {
                        window.requestAnimationFrame(step);
                    }
                };
                window.requestAnimationFrame(step);
            };

            const observer = new IntersectionObserver(entries => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const stat1 = document.getElementById('capacity-stat');
                        const stat2 = document.getElementById('global-share-stat');
                        const stat3 = document.getElementById('investment-stat');
                        animateValue(stat1, 0, 1100, 2000);
                        animateValue(stat2, 0, 80, 2000);
                        animateValue(stat3, 0, 13, 2000);
                        observer.unobserve(entry.target);
                    }
                });
            }, { threshold: 0.5 });
            observer.observe(document.getElementById('capacity-stat'));


            // Capacity Chart
            const ctxCapacity = document.getElementById('capacityChart').getContext('2d');
            new Chart(ctxCapacity, {
                type: 'bar',
                data: {
                    labels: ['2018', '2020', '2022', '2024', 'H1 2025'],
                    datasets: [{
                        label: 'Total Installed Solar Capacity (GW)',
                        data: [175, 253, 392, 890, 1100],
                        backgroundColor: '#B48A3D',
                        borderColor: '#a37a30',
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: { display: true, text: 'Gigawatts (GW)' }
                        }
                    },
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ` ${context.raw.toLocaleString()} GW`;
                                }
                            }
                        }
                    }
                }
            });

            // Energy Mix Chart
            const ctxMix = document.getElementById('mixChart').getContext('2d');
            new Chart(ctxMix, {
                type: 'doughnut',
                data: {
                    labels: ['Solar', 'Wind', 'Hydro', 'Other Renewables'],
                    datasets: [{
                        label: 'Renewable Mix',
                        data: [40, 30, 25, 5],
                        backgroundColor: ['#B48A3D', '#2C5F2D', '#60A5FA', '#9CA3AF'],
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom' }
                    }
                }
            });
            
            // Smooth scrolling for nav links
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                });
            });

            // Mobile navigation
            document.getElementById('mobile-nav').addEventListener('change', function(e) {
                 document.querySelector(e.target.value).scrollIntoView({
                        behavior: 'smooth'
                    });
            });

            // Active nav link highlighting on scroll
            const sections = document.querySelectorAll('section');
            const navLi = document.querySelectorAll('header nav a');
            window.addEventListener('scroll', ()=> {
                let current = '';
                sections.forEach( section => {
                    const sectionTop = section.offsetTop;
                    const sectionHeight = section.clientHeight;
                    if(pageYOffset >= (sectionTop - sectionHeight / 3)){
                        current = section.getAttribute('id');
                    }
                })
                
                navLi.forEach( a => {
                    a.classList.remove('active');
                    if(a.getAttribute('href') == `#${current}`){
                        a.classList.add('active');
                    }
                })
            });
        });

        // Toggle function for tech cards
        function toggleDetails(element) {
            element.classList.toggle('open');
            const icon = element.querySelector('span');
            icon.style.transform = element.classList.contains('open') ? 'rotate(45deg)' : 'rotate(0)';
        }

    </script>
</body>
</html>

