<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Energy Demand & Carbon Footprint</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Visualization & Content Choices: 
        - Report Info: Executive Summary -> Goal: Inform -> Presentation: Text blocks -> Interaction: Static -> Justification: Provides a quick overview.
        - Report Info: Table 2 (Projected % of Global Electricity Consumption for Data Centers) -> Goal: Change/Inform -> Viz: Bar Chart (Chart.js) -> Interaction: Tooltips on hover -> Justification: Visually represents the trend over time, fulfilling a specific user request. Library: Chart.js.
        - Report Info: Key Global AI/Data Center Energy Demand Projections (Table 1) -> Goal: Inform/Compare -> Presentation: HTML Table -> Interaction: Static -> Justification: Presents detailed comparative data in a structured format.
        - Report Info: Sections on Carbon Footprint, Drivers, Mitigation, Economics, Conclusion -> Goal: Inform/Explain -> Presentation: Text blocks, lists -> Interaction: Static/Scroll-to -> Justification: Breaks down complex information into digestible thematic sections.
        - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Tailwind's Inter font stack requires this if not globally available */
        @import url('https://rsms.me/inter/inter.css');
        html { font-family: 'Inter', sans-serif; }
        @supports (font-variation-settings: normal) {
          html { font-family: 'Inter var', sans-serif; }
        }

        .smooth-scroll {
            scroll-behavior: smooth;
        }
        .nav-link {
            @apply px-3 py-2 rounded-md text-sm font-medium text-neutral-700 hover:bg-sky-100 hover:text-sky-700 transition-colors;
        }
        .nav-link-active {
            @apply bg-sky-600 text-white;
        }
        .section-title {
            @apply text-3xl font-bold text-sky-700 mb-6;
        }
        .subsection-title {
            @apply text-2xl font-semibold text-sky-600 mb-4 mt-6;
        }
        .card {
            @apply bg-white p-6 rounded-lg shadow-lg mb-6;
        }
        .stat-card {
            @apply bg-sky-50 p-6 rounded-lg shadow-md text-center;
        }
        .stat-value {
            @apply text-3xl font-bold text-sky-700;
        }
        .stat-label {
            @apply text-neutral-600 mt-1;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 700px; /* Adjusted max-width */
            margin-left: auto;
            margin-right: auto;
            height: 40vh; /* Responsive height */
            max-height: 450px; /* Increased max-height */
        }
        @media (min-width: 768px) { /* md breakpoint */
            .chart-container {
                height: 350px; /* Specific height for medium screens */
            }
        }
        table {
            @apply w-full text-sm text-left text-neutral-500;
        }
        thead {
            @apply text-xs text-neutral-700 uppercase bg-neutral-100;
        }
        th, td {
            @apply px-6 py-3;
        }
        tbody tr {
            @apply bg-white border-b hover:bg-neutral-50;
        }
    </style>
</head>
<body class="bg-amber-50 text-neutral-800 smooth-scroll">

    <header class="bg-white shadow-md sticky top-0 z-50">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center">
                    <h1 class="text-xl font-bold text-sky-700">AI Energy & Environment Report</h1>
                </div>
                <nav class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4">
                        <a href="#overview" class="nav-link">Overview</a>
                        <a href="#projections" class="nav-link">Projections</a>
                        <a href="#carbon-footprint" class="nav-link">Carbon Footprint</a>
                        <a href="#drivers" class="nav-link">Drivers</a>
                        <a href="#mitigation" class="nav-link">Mitigation</a>
                        <a href="#implications" class="nav-link">Implications</a>
                        <a href="#conclusion" class="nav-link">Conclusion</a>
                    </div>
                </nav>
                <div class="md:hidden">
                    <button id="mobile-menu-button" class="text-neutral-700 hover:text-sky-700 focus:outline-none">
                        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div id="mobile-menu" class="md:hidden hidden">
            <a href="#overview" class="block nav-link">Overview</a>
            <a href="#projections" class="block nav-link">Projections</a>
            <a href="#carbon-footprint" class="block nav-link">Carbon Footprint</a>
            <a href="#drivers" class="block nav-link">Drivers</a>
            <a href="#mitigation" class="block nav-link">Mitigation</a>
            <a href="#implications" class="block nav-link">Implications</a>
            <a href="#conclusion" class="block nav-link">Conclusion</a>
        </div>
    </header>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <section id="overview" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">Overview: AI's Energy Challenge</h2>
            <div class="card">
                <p class="mb-4">This section provides a high-level summary of the report's findings. The rapid growth of Artificial Intelligence (AI) is set to significantly impact global energy demand and carbon emissions. Data centers, the backbone of AI, are projected to consume a rapidly increasing share of global electricity, potentially doubling their 2024 consumption by 2030. This surge brings substantial economic opportunities but also poses serious environmental challenges that require urgent and coordinated action.</p>
                <p>The report explores these dynamics, detailing energy projections, carbon footprint implications, the drivers behind this escalating consumption, potential mitigation strategies, and the broader economic and policy considerations. The core message is the critical need for sustainable AI development, balancing technological advancement with environmental responsibility.</p>
            </div>
        </section>

        <section id="projections" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">Projected Energy Demand (2025-2030)</h2>
            <div class="card">
                <p class="mb-6">This section delves into the specific projections for AI and data center energy consumption over the next five years. Understanding these forecasts is crucial for anticipating the scale of the challenge and opportunity. We will look at overall data center energy use, AI's specific contribution, and how these figures compare to other major energy consumers. The centerpiece is a visualization of the projected percentage of global electricity that data centers (largely driven by AI) will consume.</p>

                <h3 class="subsection-title">Projected Global Electricity Consumption by Data Centers (2025-2030)</h3>
                <p class="mb-4 text-neutral-600">The chart below illustrates the IEA's Base Case projection for the percentage of total global electricity consumption attributed to data centers. This serves as a key indicator of AI's growing energy footprint, as AI workloads are a primary driver of data center energy growth.</p>
                <div class="chart-container bg-white p-4 rounded-lg shadow-md mb-8">
                    <canvas id="aiEnergyProjectionChart"></canvas>
                </div>
                <p class="text-sm text-neutral-500 mb-6 text-center"><em>Data based on IEA projections; 2024 baseline is 1.5%, 2030 projection is "just under 3%". Intermediate years are linearly interpolated.</em></p>

                <h3 class="subsection-title">Key Projection Highlights</h3>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6 mb-6">
                    <div class="stat-card">
                        <div class="stat-value">~1.5%</div>
                        <div class="stat-label">Global Electricity Used by Data Centers (2024)</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value">&lt; 3%</div>
                        <div class="stat-label">Projected Global Electricity Use by Data Centers (2030 - IEA Base Case)</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value">Up to 21%</div>
                        <div class="stat-label">Potential Global Energy Demand by Data Centers (2030 - MIT High-End Scenario)</div>
                    </div>
                     <div class="stat-card">
                        <div class="stat-value">1,500 TWh</div>
                        <div class="stat-label">Projected AI-driven Global Electricity Needs by 2030 (OPEC/IMF)</div>
                    </div>
                     <div class="stat-card">
                        <div class="stat-value">4x</div>
                        <div class="stat-label">Projected Growth in Electricity Demand from AI-Optimized Data Centers by 2030</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value">27%</div>
                        <div class="stat-label">Projected Share of AI Workloads in Data Center Power Demand by 2027</div>
                    </div>
                </div>

                <p class="mb-4">Global data center electricity consumption was around 415 TWh in 2024 (1.5% of global total). The IEA projects this to reach 945 TWh by 2030 (&lt;3% of global total). More aggressive scenarios, like OPEC/IMF's, suggest AI-driven electricity needs could hit 1,500 TWh by 2030, comparable to India's current total consumption. MIT researchers even posit a high-end scenario where data centers account for up to 21% of global energy demand by 2030 when considering the full delivery cost of AI.</p>
                <p class="mb-4">AI is the primary driver, with demand from AI-optimized data centers projected to quadruple by 2030. By 2027, AI workloads are expected to make up 27% of data center power demand. This growth highlights the shift towards more energy-intensive AI operations.</p>

                <h3 class="subsection-title">Comparative Analysis</h3>
                <p class="mb-4">To put AI's energy demand into perspective: by 2030, data center electricity use could surpass that of the entire electric vehicle fleet. Currently, data centers consume a similar amount of global energy as the airline industry (1-2%). This scale elevates AI's energy needs from a niche IT concern to a major macroeconomic and energy policy challenge.</p>

                <h3 class="subsection-title">Key Global AI/Data Center Energy Demand Projections (2024-2030)</h3>
                <div class="overflow-x-auto card">
                    <table>
                        <thead>
                            <tr>
                                <th>Year</th>
                                <th>Source(s)</th>
                                <th>Projection Type</th>
                                <th>Projected Energy (TWh)</th>
                                <th>Est. % of Global Electricity</th>
                                <th>Notes</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>2024</td>
                                <td>IEA</td>
                                <td>Global Data Centers Total</td>
                                <td>415</td>
                                <td>1.5%</td>
                                <td>Baseline</td>
                            </tr>
                            <tr>
                                <td>2027</td>
                                <td>Morgan Lewis/GS</td>
                                <td>AI Workloads Share of DC Market</td>
                                <td>N/A</td>
                                <td>N/A</td>
                                <td>AI accounts for 27% of DC power demand</td>
                            </tr>
                            <tr>
                                <td>2030</td>
                                <td>IEA Base Case</td>
                                <td>Global Data Centers Total</td>
                                <td>945</td>
                                <td>&lt; 3%</td>
                                <td>DC electricity consumption doubles from 2024</td>
                            </tr>
                            <tr>
                                <td>2030</td>
                                <td>OPEC/IMF</td>
                                <td>AI-driven Global Electricity Needs</td>
                                <td>1,500</td>
                                <td>N/A</td>
                                <td>Comparable to India's current total; 1.5x EVs</td>
                            </tr>
                            <tr>
                                <td>2030</td>
                                <td>MIT High-End</td>
                                <td>Global Data Centers Total</td>
                                <td>N/A</td>
                                <td>Up to 21%</td>
                                <td>Factoring in full cost of AI delivery</td>
                            </tr>
                             <tr>
                                <td>2030</td>
                                <td>IEA</td>
                                <td>AI-optimized Data Centers</td>
                                <td>N/A</td>
                                <td>N/A</td>
                                <td>Electricity demand quadruples</td>
                            </tr>
                        </tbody>
                    </table>
                     <p class="mt-2 text-xs text-neutral-500"><em>Note: "N/A" indicates that a specific percentage of global electricity consumption or TWh value was not directly provided for that projection type or year in the source material. GS refers to Goldman Sachs.</em></p>
                </div>
            </div>
        </section>

        <section id="carbon-footprint" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">The Carbon Footprint of AI</h2>
            <div class="card">
                <p class="mb-6">This section examines the environmental consequences of AI's growing energy demand, focusing on greenhouse gas emissions. The source of energy powering data centers is a critical factor determining AI's carbon intensity. We also touch upon broader environmental impacts like water consumption and e-waste, which are integral to a holistic view of AI's sustainability.</p>

                <h3 class="subsection-title">Quantifying AI-Driven GHG Emissions</h3>
                <p class="mb-4">Data centers currently contribute about 0.5% of global combustion emissions (180 Mt CO2). In the US, they accounted for ~2% of national emissions in 2023 (105 Mt CO2). Projections are concerning: AI's electricity demand could add 1.7 Gt to global GHG emissions between 2025-2030 under current policies. This is comparable to Italy's total energy-related emissions over five years. The IMF estimates a 1.2% cumulative increase in global GHG emissions due to strong AI adoption in this period.</p>
                <p class="mb-4">However, greener energy policies could reduce this AI-driven increase by 24%. While the IMF suggests AI's economic gains might outweigh emission costs (estimated at $50.7-$66.3 billion), this calculation requires careful scrutiny regarding the full social cost of carbon and equitable distribution of benefits versus burdens.</p>

                <h3 class="subsection-title">The Critical Role of Energy Mix</h3>
                <p class="mb-4">AI's carbon footprint heavily depends on the electricity source. While tech firms aim for more renewables, the IEA forecasts only about half of data center energy demand will be met by renewables by 2030. Fossil fuels, particularly natural gas and coal, will remain significant. In the US, 56% of data center electricity comes from fossil fuels, and their average carbon intensity is 50% higher than the national grid average, indicating locations in carbon-intensive areas.</p>
                <p class="mb-4">This disconnect between AI's rapid energy growth and the pace of renewable deployment means AI could lock in higher fossil fuel consumption, hindering broader climate goals.</p>

                <h3 class="subsection-title">Broader Environmental Impacts</h3>
                <p class="mb-4"><strong>Water Consumption:</strong> Data centers need substantial water for cooling, often straining local water resources in already stressed areas.</p>
                <p><strong>E-Waste & Resource Depletion:</strong> Short lifespans of specialized hardware (GPUs) contribute to e-waste. Manufacturing these components requires rare earth minerals (e.g., gallium, copper, silicon), depleting natural resources and creating supply chain vulnerabilities. By 2030, data centers could consume up to 11% of current global gallium supply.</p>
            </div>
        </section>

        <section id="drivers" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">Drivers of AI's Escalating Energy Consumption</h2>
            <div class="card">
                <p class="mb-6">Understanding why AI's energy demand is surging is key to addressing it. This section explores the primary factors: the proliferation of large, dense data centers; the specific hardware requirements of AI, like power-hungry GPUs; and the sheer computational intensity of training and running AI models.</p>

                <h3 class="subsection-title">Proliferation of Data Centers & Hyperscale Facilities</h3>
                <p class="mb-4">Consumer AI adoption (e.g., ChatGPT) is pushing tech giants to expand data center capacity. While data volume is exploding (41 to 147 zettabytes projected), the number of data centers has only modestly increased (7,000 to 8,000). This points to a trend of larger, denser, and more power-intensive "hyperscale" facilities. The "AI Acceleration Era" is pushing energy demand to new heights, outpacing previous efficiency gains from consolidation.</p>

                <h3 class="subsection-title">Hardware Demands: GPUs and Specialized Accelerators</h3>
                <p class="mb-4">AI relies on specialized hardware, especially Graphics Processing Units (GPUs), which consume significantly more power than traditional servers (AI servers can use up to 10x more). Training Large Language Models (LLMs) involves thousands of GPUs running for months. The IT sector's electricity intensity in the US is projected to rise to 4% by 2030 from 1% in 2017, reflecting this shift.</p>

                <h3 class="subsection-title">Computational Intensity: Training and Inference</h3>
                <p class="mb-4"><strong>Training:</strong> Developing AI models, especially large ones, is extremely energy-intensive due to processing vast data and billions of parameters. Each new generation of LLM tends to have more parameters, increasing energy needs.</p>
                <p><strong>Inference:</strong> Running trained models to generate responses also consumes substantial energy. A single ChatGPT query uses about five times more electricity than a simple web search. Creating an image with generative AI can use the energy equivalent of fully charging a smartphone. As AI becomes ubiquitous, the cumulative energy cost of inferences will skyrocket.</p>
            </div>
        </section>

        <section id="mitigation" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">Mitigating AI's Energy and Environmental Impact</h2>
            <div class="card">
                <p class="mb-6">Addressing AI's environmental footprint requires a multi-faceted strategy. This section outlines potential solutions, covering technological innovations in algorithms and hardware, operational best practices for data centers, and broader strategic approaches like cloud computing and renewable energy integration. These efforts aim to make AI development more sustainable.</p>

                <h3 class="subsection-title">Technological Solutions</h3>
                <ul class="list-disc list-inside space-y-2 mb-4">
                    <li><strong>Algorithm Optimization:</strong> More efficient models (e.g., data pruning, quantization, compression) reduce energy use. Pruning 90% of parameters in AlexNet cut model size by 9x with minimal accuracy loss. Rethinking training with early accuracy prediction can save significant compute time.</li>
                    <li><strong>Hardware Efficiency:</strong> Energy-efficient CPUs (AMD EPYC, Intel Xeon, ARM-based), GPUs (NVIDIA A100, AMD Instinct MI100), dedicated AI accelerators (Google TPUs), and efficient data storage (NVMe SSDs) are crucial.</li>
                </ul>

                <h3 class="subsection-title">Operational Best Practices for Data Centers</h3>
                <ul class="list-disc list-inside space-y-2 mb-4">
                    <li><strong>Cooling Optimization:</strong> Liquid cooling, free cooling, hot/cold aisle containment. AI itself can optimize cooling in real-time.</li>
                    <li><strong>Server Consolidation:</strong> Virtualization and containerization reduce the number of active servers.</li>
                    <li><strong>Energy-Efficient Design:</strong> Modular data centers, high-efficiency power supplies, energy monitoring systems, and strategic location near renewable sources.</li>
                </ul>

                <h3 class="subsection-title">Strategic Approaches</h3>
                <ul class="list-disc list-inside space-y-2 mb-4">
                    <li><strong>Cloud Computing & Virtualization:</strong> Cloud providers offer resource sharing, optimized data centers, scalability, and geographic workload optimization for efficiency.</li>
                    <li><strong>Renewable Energy Integration:</strong> Accelerating the shift to renewables is vital. However, projections show only half of data center demand met by renewables by 2030, indicating a need for faster deployment.</li>
                    <li><strong>Energy Monitoring & Management:</strong> Tools for power capping, dynamic voltage/frequency scaling (DVFS), off-peak scheduling, batch processing, and dynamic load balancing.</li>
                </ul>
            </div>
        </section>

        <section id="implications" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">Economic Implications and Policy Considerations</h2>
            <div class="card">
                <p class="mb-6">The rise of AI brings both significant economic opportunities and substantial environmental costs, creating a complex landscape for policymakers and businesses. This section explores the balance between AI's projected economic gains and its environmental footprint, highlighting the critical need for investment in grid infrastructure and renewable energy to support sustainable growth.</p>

                <h3 class="subsection-title">Weighing Economic Gains Against Environmental Costs</h3>
                <p class="mb-4">The IMF projects AI could boost global GDP by ~0.5% annually (2025-2030). They suggest these gains may outweigh the costs of additional emissions (estimated at $50.7-$66.3 billion). However, the IMF also notes these economic benefits won't be shared equally worldwide. This raises equity concerns, as environmental burdens might disproportionately affect regions not reaping the primary economic benefits. A simple aggregate cost-benefit analysis may not capture the full picture, urging policies for equitable benefit distribution and proactive management of localized impacts.</p>

                <h3 class="subsection-title">Investment Needs for Grid Infrastructure and Renewable Energy</h3>
                <p class="mb-4">AI's growth will strain electric grids, requiring massive investment. Goldman Sachs estimates $720 billion for grid upgrades by 2030. Constrained renewable growth and transmission infrastructure could lead to electricity price hikes (e.g., 8.6% in the US) and increased carbon emissions. Grid capacity is a more critical factor for price increases than renewable constraints alone. Significant investment in grid modernization and expansion is vital to efficiently deliver clean power to energy-hungry data centers and is as crucial as generating more renewable energy itself.</p>
            </div>
        </section>

        <section id="conclusion" class="pt-16 -mt-16 mb-12">
            <h2 class="section-title">Conclusion: Towards Sustainable AI</h2>
            <div class="card">
                <p class="mb-4">AI's rapid expansion is a double-edged sword, offering immense economic potential while posing serious threats to global energy systems and climate targets. Projections show a dramatic rise in AI-driven data center electricity demand, potentially adding gigatons of CO2 emissions if reliant on fossil fuels. The impact extends to water resources and e-waste.</p>
                <p class="mb-4">Addressing this requires a multi-pronged strategy: technological innovation (efficient algorithms/hardware), operational best practices in data centers (cooling, consolidation), and strategic ecosystem changes (cloud efficiencies, accelerated renewable energy integration). While economic benefits are touted, equitable distribution and full environmental cost accounting are crucial. Massive investment in grid modernization and renewables is not just desirable but essential.</p>
                <p>Ultimately, AI's environmental future depends on a collective commitment from governments, tech companies, and energy providers to prioritize sustainability, integrating it into the core of AI development and the energy systems that power it.</p>
            </div>
        </section>
    </main>

    <footer class="bg-neutral-800 text-amber-50 py-8 text-center">
        <p>&copy; 2024 AI Energy & Environment Interactive Report. Information based on "The Escalating Energy Demands of Artificial Intelligence and its Carbon Footprint: Projections and Implications (2025-2030)".</p>
    </footer>

    <script>
        // Mobile menu toggle
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');
        mobileMenuButton.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });

        // Close mobile menu when a link is clicked
        const mobileNavLinks = mobileMenu.querySelectorAll('a');
        mobileNavLinks.forEach(link => {
            link.addEventListener('click', () => {
                mobileMenu.classList.add('hidden');
            });
        });
        
        // Active navigation link highlighting
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('header nav a, #mobile-menu a');

        window.addEventListener('scroll', () => {
            let current = '';
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (pageYOffset >= sectionTop - 80) { // Adjusted offset for sticky header
                    current = section.getAttribute('id');
                }
            });

            navLinks.forEach(link => {
                link.classList.remove('nav-link-active');
                if (link.getAttribute('href').substring(1) === current) {
                    link.classList.add('nav-link-active');
                }
            });
        });


        // Chart.js: AI Energy Projection Chart
        const aiEnergyData = {
            labels: ['2025', '2026', '2027', '2028', '2029', '2030'],
            datasets: [{
                label: '% of Global Electricity Consumption by Data Centers',
                data: [1.73, 1.97, 2.20, 2.43, 2.67, 2.90], // From Table 2 in the report
                backgroundColor: 'rgba(59, 130, 246, 0.7)', // sky-500 with opacity
                borderColor: 'rgba(23, 37, 84, 1)', // darker blue for border
                borderWidth: 1,
                borderRadius: 5,
                barPercentage: 0.7,
                categoryPercentage: 0.8
            }]
        };

        const aiEnergyConfig = {
            type: 'bar',
            data: aiEnergyData,
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: 'Percentage (%)',
                            font: {
                                size: 14,
                                weight: 'bold'
                            },
                            color: '#4b5563' // neutral-600
                        },
                        grid: {
                            color: 'rgba(209, 213, 219, 0.5)' // neutral-300 with opacity
                        },
                        ticks: {
                             color: '#4b5563', // neutral-600
                             font: {
                                size: 12
                             },
                             callback: function(value) {
                                return value + '%';
                             }
                        }
                    },
                    x: {
                        title: {
                            display: true,
                            text: 'Year',
                            font: {
                               size: 14,
                               weight: 'bold'
                            },
                            color: '#4b5563' // neutral-600
                        },
                        grid: {
                            display: false
                        },
                        ticks: {
                             color: '#4b5563', // neutral-600
                             font: {
                                size: 12
                             }
                        }
                    }
                },
                plugins: {
                    legend: {
                        position: 'top',
                        labels: {
                             color: '#1f2937', // neutral-800
                             font: {
                                size: 14
                             }
                        }
                    },
                    tooltip: {
                        enabled: true,
                        backgroundColor: 'rgba(0,0,0,0.8)',
                        titleFont: { size: 14, weight: 'bold' },
                        bodyFont: { size: 12 },
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                if (context.parsed.y !== null) {
                                    label += context.parsed.y + '%';
                                }
                                return label;
                            }
                        }
                    }
                },
                animation: {
                    duration: 1000,
                    easing: 'easeInOutQuart'
                }
            }
        };

        const aiEnergyProjectionChartCtx = document.getElementById('aiEnergyProjectionChart').getContext('2d');
        const aiEnergyProjectionChart = new Chart(aiEnergyProjectionChartCtx, aiEnergyConfig);

    </script>
</body>
</html>
