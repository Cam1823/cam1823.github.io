<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Our Next Adventure: A Year in Annapolis & Brooklyn</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&family=Lora:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
    <style>
        html {
            scroll-behavior: smooth;
        }
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #FDFBF7; /* Warm Cream */
            color: #333;
        }
        h1, h2, h3 {
            font-family: 'Poppins', sans-serif;
            font-weight: 700;
        }
        .lora-font {
            font-family: 'Lora', serif;
        }
        .section-card {
            background-color: white;
            border-radius: 1.5rem;
            padding: 2.5rem;
            margin-bottom: 2rem;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.04);
            border: 1px solid #F0EFEA;
        }
        .bg-navy { background-color: #1A3A5A; }
        .text-navy { color: #1A3A5A; }
        .bg-sage { background-color: #8A9A5B; }
        .text-sage { color: #8A9A5B; }
        .bg-cream { background-color: #FDFBF7; }
        .text-cream { color: #FDFBF7; }

        /* Nav Menu Styles */
        #menu-button {
            position: fixed;
            top: 1rem;
            left: 1rem;
            z-index: 100;
            background-color: white;
            border-radius: 9999px;
            padding: 0.75rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            transition: all 0.2s ease-in-out;
        }
        #menu-button:hover {
            transform: scale(1.1);
        }
        #nav-menu {
            position: fixed;
            top: 0;
            left: 0;
            height: 100%;
            width: 280px;
            background-color: #1A3A5A;
            z-index: 90;
            transform: translateX(-100%);
            transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            padding: 4rem 2rem 2rem;
        }
        #nav-menu.is-open {
            transform: translateX(0);
        }
        .nav-link {
            display: block;
            padding: 0.75rem 1rem;
            color: white;
            font-weight: 600;
            border-radius: 0.5rem;
            transition: background-color 0.2s;
        }
        .nav-link:hover {
            background-color: rgba(255, 255, 255, 0.1);
        }
        #page-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 80;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease-in-out;
        }
        #page-overlay.is-visible {
            opacity: 1;
            pointer-events: auto;
        }


        /* Custom styles for slider */
        input[type=range] {
            -webkit-appearance: none;
            appearance: none;
            width: 100%;
            cursor: pointer;
            background: transparent;
        }
        input[type=range]:focus {
            outline: none;
        }
        input[type=range]::-webkit-slider-runnable-track {
            height: 8px;
            background: #e2e8f0;
            border-radius: 4px;
        }
        input[type=range]::-moz-range-track {
            height: 8px;
            background: #e2e8f0;
            border-radius: 4px;
        }
        input[type=range]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            margin-top: -6px; /* center thumb on track */
            background-color: #1A3A5A;
            height: 20px;
            width: 20px;
            border-radius: 50%;
            border: 2px solid white;
            box-shadow: 0 0 5px rgba(0,0,0,0.2);
        }
        input[type=range]::-moz-range-thumb {
            background-color: #1A3A5A;
            height: 20px;
            width: 20px;
            border-radius: 50%;
            border: 2px solid white;
            box-shadow: 0 0 5px rgba(0,0,0,0.2);
        }
        .token {
            transition: all 0.3s ease-in-out;
        }
        
        /* To-do list styling */
        input[type="checkbox"]:checked + label {
            text-decoration: line-through;
            color: #9ca3af; /* gray-400 */
        }
        /* Calendar Styling */
        .calendar-event {
            font-size: 0.8rem;
            padding: 0.25rem 0.5rem;
            border-radius: 0.375rem;
            margin-bottom: 0.5rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .event-travel { background-color: #1A3A5A; color: white; }
        .event-social { background-color: #8A9A5B; color: white; }
        .event-work { background-color: #e2e8f0; color: #4a5568; }
        .event-flex { background-color: #EAD3A2; color: #785a12; }
        .remove-event {
            cursor: pointer;
            font-weight: bold;
            margin-left: 0.5rem;
            opacity: 0.6;
        }
        .remove-event:hover {
            opacity: 1;
        }
        /* Winner Modal Styles from Spin the Wheel */
        .modal-hidden {
            display: none;
        }
        .modal-visible {
            display: flex;
        }
        #modalContent {
            animation: scaleUp 0.5s cubic-bezier(0.165, 0.840, 0.440, 1.000) forwards;
        }
        @keyframes scaleUp {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        .pointer {
            width: 0;
            height: 0;
            border-left: 20px solid transparent;
            border-right: 20px solid transparent;
            border-top: 30px solid #dc2626; /* red-600 */
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10;
        }
        .gemini-output {
            background-color: #f7fafc;
            border-left: 4px solid #1A3A5A;
            padding: 1rem;
            margin-top: 1rem;
            border-radius: 0.5rem;
            white-space: pre-wrap;
            font-family: 'Lora', serif;
        }
        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #1A3A5A;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            margin: 1rem auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="antialiased">

    <!-- Navigation Menu -->
    <button id="menu-button" aria-label="Open navigation menu">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-navy" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
        </svg>
    </button>
    <div id="page-overlay"></div>
    <nav id="nav-menu">
        <ul class="space-y-2">
            <li><a href="#briefing" class="nav-link">Adventure Briefing</a></li>
            <li><a href="#homes" class="nav-link">Our Two Homes</a></li>
            <li><a href="#commute" class="nav-link">The Weekly Commute</a></li>
            <li><a href="#weekly-life" class="nav-link">Our Weekly Life</a></li>
            <li><a href="#planner" class="nav-link">Weekly Planner</a></li>
            <li><a href="#flex-fund" class="nav-link">Flex Time Fund</a></li>
            <li><a href="#numbers" class="nav-link">Year in Numbers</a></li>
            <li><a href="#year-together" class="nav-link">Our Year Together</a></li>
            <li><a href="#todos" class="nav-link">Next Steps</a></li>
            <li><a href="#spinner" class="nav-link">Spin for Fun!</a></li>
        </ul>
    </nav>
    

    <div class="max-w-4xl mx-auto p-4 md:p-8">
        
        <!-- Header -->
        <header class="text-center mb-10">
            <h1 class="text-4xl md:text-5xl font-bold text-navy lora-font">Our Next Adventure</h1>
            <p class="text-xl md:text-2xl text-gray-500 mt-2">A Year in Annapolis & Brooklyn</p>
        </header>
        
        <!-- Section 1: The Adventure Briefing -->
        <section id="briefing" class="section-card text-center bg-navy/5">
            <h2 class="text-2xl font-bold text-center mb-6">The Adventure Briefing</h2>
            <p class="text-gray-700 max-w-2xl mx-auto lora-font italic">An executive summary of the year ahead, balancing city hustle with suburban calm, quality time with social fun, and planned routines with spontaneous adventures.</p>
            <div class="mt-6 grid grid-cols-2 md:grid-cols-4 gap-4 text-navy">
                <div class="font-semibold">
                    <div class="text-3xl">2</div>
                    <div class="text-sm">Homes</div>
                </div>
                <div class="font-semibold">
                    <div class="text-3xl">7</div>
                    <div class="text-sm">Weddings</div>
                </div>
                <div class="font-semibold">
                    <div class="text-3xl">~80%</div>
                    <div class="text-sm">Time Together</div>
                </div>
                <div class="font-semibold">
                    <div class="text-3xl">52</div>
                    <div class="text-sm">Commutes</div>
                </div>
            </div>
        </section>

        <!-- Section 2: Our Two Homes -->
        <section id="homes" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">Our Two Homes</h2>
            <div class="grid md:grid-cols-2 gap-8 items-start">
                <!-- Annapolis House -->
                <div class="text-center border-r-0 md:border-r md:pr-8 border-gray-200">
                    <div class="text-5xl mb-3">🏡</div>
                    <h3 class="text-xl font-bold">Annapolis House</h3>
                    <p class="text-gray-500">Net Monthly Cost: <span class="font-semibold text-gray-700">$1,250</span></p>
                    <div class="mt-4 text-left text-sm bg-sage/10 p-4 rounded-lg">
                        <h4 class="font-bold text-sage mb-2">Perks & Bennies:</h4>
                        <ul class="space-y-1 text-gray-700">
                            <li class="flex items-start"><span class="mr-2 text-sage">✓</span> A yard for a puppy!</li>
                            <li class="flex items-start"><span class="mr-2 text-sage">✓</span> Close to family</li>
                            <li class="flex items-start"><span class="mr-2 text-sage">✓</span> Lower cost of living</li>
                        </ul>
                    </div>
                </div>
                <!-- Brooklyn Apartment -->
                <div class="text-center">
                     <div class="text-5xl mb-3">🏙️</div>
                    <h3 class="text-xl font-bold">Brooklyn Apartment</h3>
                    <p class="text-gray-500">Monthly Rent: <span class="font-semibold text-gray-700">$5,700</span></p>
                     <div class="mt-4 text-left text-sm bg-navy/10 p-4 rounded-lg">
                        <h4 class="font-bold text-navy mb-2">Perks & Bennies:</h4>
                        <ul class="space-y-1 text-gray-700">
                           <li class="flex items-start"><span class="mr-2 text-navy">✓</span> In the middle of the action</li>
                           <li class="flex items-start"><span class="mr-2 text-navy">✓</span> Close to work & friends</li>
                           <li class="flex items-start"><span class="mr-2 text-navy">✓</span> A dynamite view</li>
                        </ul>
                    </div>
                </div>
            </div>
            <div class="text-center mt-8 pt-6 border-t border-gray-200">
                <p class="text-lg font-bold">Total Monthly Housing: <span class="text-navy text-2xl">$6,950</span></p>
            </div>
        </section>

        <!-- Section 3: The Weekly Commute -->
        <section id="commute" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">The Weekly Commute: Train vs. Car</h2>
            <div class="grid md:grid-cols-2 gap-8">
                <!-- Train Travel -->
                <div class="bg-navy/5 p-6 rounded-lg">
                    <div class="flex items-center justify-center space-x-3 mb-4">
                        <span class="text-2xl">🚆</span>
                        <h3 class="text-xl font-bold">Train Travel</h3>
                    </div>
                    <p class="text-center text-2xl font-bold text-navy mb-4">~$300 <span class="text-sm font-normal">/ week</span></p>
                    <div class="text-sm space-y-2 mb-4">
                        <p class="font-semibold text-gray-700">Cost Breakdown:</p>
                        <p class="text-gray-600">Based on a 10-ride pass for $750 (5 round trips).</p>
                    </div>
                    <div class="space-y-2 text-sm">
                        <p class="flex items-start"><span class="text-green-600 mr-2 mt-1">✓</span><strong>Pros:</strong> Relaxing, predictable, can work on the go.</p>
                        <p class="flex items-start"><span class="text-red-500 mr-2 mt-1">✗</span><strong>Cons:</strong> Fixed schedules, travel to/from the station.</p>
                    </div>
                </div>
                <!-- Driving -->
                <div class="bg-sage/5 p-6 rounded-lg">
                    <div class="flex items-center justify-center space-x-3 mb-4">
                         <span class="text-2xl">🚗</span>
                        <h3 class="text-xl font-bold">Driving</h3>
                    </div>
                     <p class="text-center text-2xl font-bold text-sage mb-4">~$310 <span class="text-sm font-normal">/ week</span></p>
                    <div class="text-sm space-y-1 mb-4">
                        <p class="font-semibold text-gray-700">Cost Breakdown:</p>
                        <ul class="list-disc list-inside text-gray-600">
                            <li>Parking: ~$180</li>
                            <li>Gas: ~$60</li>
                            <li>Tolls: ~$70</li>
                        </ul>
                    </div>
                    <div class="space-y-2 text-sm">
                        <p class="flex items-start"><span class="text-green-600 mr-2 mt-1">✓</span><strong>Pros:</strong> Flexible timing, can carry more luggage.</p>
                        <p class="flex items-start"><span class="text-red-500 mr-2 mt-1">✗</span><strong>Cons:</strong> City traffic, stressful, vehicle wear & tear.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 4: Our Weekly Life -->
        <section id="weekly-life" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">Our Weekly Life</h2>
            <div class="flex justify-center items-center space-x-4 md:space-x-8 mb-10 text-center">
                <div class="font-semibold">
                    <div class="text-3xl">🏙️</div>
                    <p>Mon - Thurs</p>
                    <p class="font-bold text-navy">Brooklyn Life</p>
                </div>
                <div class="text-gray-300 font-light text-3xl">→</div>
                 <div class="font-semibold">
                    <div class="text-3xl">🏡</div>
                    <p>Thurs - Sun</p>
                    <p class="font-bold text-sage">Annapolis Life</p>
                </div>
            </div>
            <div class="pt-8 border-t border-gray-200">
                <h3 class="text-xl font-bold text-center mb-6">How We Spend Our Evenings</h3>
                <div class="max-w-md mx-auto space-y-4 text-left">
                    <div class="flex items-center"><span class="text-2xl mr-4">❤️</span><span><strong>2 Nights/Week:</strong> Dedicated Quality Time (Cooking, date nights)</span></div>
                    <div class="flex items-center"><span class="text-2xl mr-4">📺</span><span><strong>1 Night/Week:</strong> Friends Together (Watching games, group dinners)</span></div>
                    <div class="flex items-center"><span class="text-2xl mr-4">🕺💃</span><span><strong>1 Night (avg):</strong> Boys/Girls Night Out (Happening every other week)</span></div>
                </div>
            </div>
        </section>

        <!-- Section: Weekly Calendar -->
        <section id="planner" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">Our Weekly Planner</h2>
            <div id="add-event-form" class="mb-8 p-6 bg-gray-50 rounded-lg">
                <h3 class="font-bold text-lg mb-4 text-center">Add a New Event</h3>
                <div class="grid md:grid-cols-4 gap-4 items-end">
                    <div class="col-span-2 md:col-span-1">
                        <label for="event-name" class="block text-sm font-medium text-gray-700">Event</label>
                        <input type="text" id="event-name" placeholder="Dinner with friends" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-navy focus:ring-navy sm:text-sm">
                    </div>
                    <div>
                        <label for="event-day" class="block text-sm font-medium text-gray-700">Day</label>
                        <select id="event-day" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-navy focus:ring-navy sm:text-sm">
                            <option>Monday</option>
                            <option>Tuesday</option>
                            <option>Wednesday</option>
                            <option>Thursday</option>
                            <option>Friday</option>
                            <option>Saturday</option>
                            <option>Sunday</option>
                        </select>
                    </div>
                    <div>
                        <label for="event-type" class="block text-sm font-medium text-gray-700">Type</label>
                        <select id="event-type" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-navy focus:ring-navy sm:text-sm">
                            <option value="travel">Travel 🚆</option>
                            <option value="social">Social 🕺</option>
                            <option value="work">Work 💼</option>
                            <option value="flex">Flex Plan ⚡️</option>
                        </select>
                    </div>
                    <button id="add-event-btn" class="bg-navy text-white font-bold py-2 px-4 rounded-md hover:bg-navy/90 transition-colors w-full">Add Event</button>
                </div>
            </div>
            <div id="calendar-grid" class="grid grid-cols-2 md:grid-cols-7 gap-2">
                <div class="day-col" id="calendar-monday">
                    <h4 class="font-bold text-center p-2 bg-gray-100 rounded-t-md">Mon</h4>
                    <div class="p-2 min-h-[150px] bg-gray-50 rounded-b-md space-y-2"></div>
                </div>
                <div class="day-col" id="calendar-tuesday">
                    <h4 class="font-bold text-center p-2 bg-gray-100 rounded-t-md">Tue</h4>
                    <div class="p-2 min-h-[150px] bg-gray-50 rounded-b-md space-y-2"></div>
                </div>
                <div class="day-col" id="calendar-wednesday">
                    <h4 class="font-bold text-center p-2 bg-gray-100 rounded-t-md">Wed</h4>
                    <div class="p-2 min-h-[150px] bg-gray-50 rounded-b-md space-y-2"></div>
                </div>
                <div class="day-col" id="calendar-thursday">
                    <h4 class="font-bold text-center p-2 bg-gray-100 rounded-t-md">Thu</h4>
                    <div class="p-2 min-h-[150px] bg-gray-50 rounded-b-md space-y-2"></div>
                </div>
                <div class="day-col" id="calendar-friday">
                    <h4 class="font-bold text-center p-2 bg-gray-100 rounded-t-md">Fri</h4>
                    <div class="p-2 min-h-[150px] bg-gray-50 rounded-b-md space-y-2"></div>
                </div>
                <div class="day-col" id="calendar-saturday">
                    <h4 class="font-bold text-center p-2 bg-sage/20 rounded-t-md">Sat</h4>
                    <div class="p-2 min-h-[150px] bg-sage/10 rounded-b-md space-y-2"></div>
                </div>
                <div class="day-col" id="calendar-sunday">
                    <h4 class="font-bold text-center p-2 bg-sage/20 rounded-t-md">Sun</h4>
                    <div class="p-2 min-h-[150px] bg-sage/10 rounded-b-md space-y-2"></div>
                </div>
            </div>
        </section>
        
        <!-- Section: Our "Flex Time" Fund -->
        <section id="flex-fund" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">Our "Flex Time" Fund: Planning for the Unplanned</h2>
            <div class="grid md:grid-cols-2 gap-8 items-center">
                <div class="relative w-48 h-64 bg-blue-100/30 rounded-t-full rounded-b-lg mx-auto border-4 border-navy p-2 flex flex-col-reverse items-center">
                    <div id="token-container" class="w-full flex flex-col-reverse gap-2 items-center">
                        <div class="token w-12 h-12 bg-yellow-400 rounded-full flex items-center justify-center text-xl shadow-md">🍻</div>
                        <div class="token w-12 h-12 bg-pink-400 rounded-full flex items-center justify-center text-xl shadow-md">🎉</div>
                        <div class="token w-12 h-12 bg-green-400 rounded-full flex items-center justify-center text-xl shadow-md">🗓️</div>
                        <div class="token w-12 h-12 bg-purple-400 rounded-full flex items-center justify-center text-xl shadow-md">🎵</div>
                    </div>
                    <div class="absolute -top-4 bg-navy text-white text-xs font-bold px-3 py-1 rounded-full">FLEX FUND</div>
                </div>
                <div class="text-sm">
                    <p class="mb-4 text-gray-700">Each month, we have a 'fund' of Flex Tokens to 'spend' on spontaneous fun. This helps us enjoy the unexpected without overwhelming our quality time.</p>
                    <p class="font-bold mb-2">Examples of what a token can be 'spent' on:</p>
                    <ul class="space-y-2 text-gray-600">
                        <li class="flex items-center"><span class="text-xl mr-2">🍻</span> Happy Hours</li>
                        <li class="flex items-center"><span class="text-xl mr-2">🎵</span> Concerts</li>
                        <li class="flex items-center"><span class="text-xl mr-2">🎉</span> Spontaneous Plans</li>
                        <li class="flex items-center"><span class="text-xl mr-2">🗓️</span> Last-Minute Plans!</li>
                    </ul>
                </div>
            </div>
             <div class="mt-8 pt-6 border-t border-gray-100">
                <label for="flex-slider" class="block text-center font-semibold text-gray-700 mb-2">How many flex nights this month?</label>
                <div class="flex items-center justify-center space-x-4">
                    <span>0</span>
                    <input id="flex-slider" type="range" min="0" max="8" value="0" class="w-full max-w-xs">
                    <span>8</span>
                </div>
                <p class="text-center text-sm text-gray-500 mt-2">Nights spent: <span id="flex-nights-value" class="font-bold text-navy">0</span></p>
            </div>
        </section>

        <!-- Section: Our Year in Numbers -->
        <section id="numbers" class="section-card bg-navy text-white text-center">
             <h2 class="text-2xl font-bold text-center mb-8">Our Year in Numbers</h2>
             <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                 <div>
                     <p class="text-4xl font-bold">365</p>
                     <p>Days</p>
                 </div>
                 <div>
                     <p class="text-4xl font-bold">52</p>
                     <p>Weekly Commutes</p>
                 </div>
                 <div>
                     <p class="text-4xl font-bold">7</p>
                     <p>Weddings Together</p>
                 </div>
                 <div>
                     <p class="text-4xl font-bold">2</p>
                     <p>Homes to Call Our Own</p>
                 </div>
             </div>
        </section>
        
        <!-- Section: Our Year Together: A Detailed Look -->
        <section id="year-together" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">Our Year Together: A Detailed Look</h2>
            <div class="w-full max-w-sm mx-auto relative">
                <canvas id="timeTogetherChart"></canvas>
            </div>
            <div class="mt-8 pt-6 border-t border-gray-200 max-w-lg mx-auto text-left space-y-3">
                <div class="flex items-start">
                    <span class="w-4 h-4 rounded-full mt-1 mr-3 flex-shrink-0" style="background-color: #1A3A5A;"></span>
                    <div>
                        <strong class="text-navy">Dedicated Quality Time:</strong>
                        <span class="text-gray-600 text-sm">Our intentional one-on-one time, like date nights and cooking together.</span>
                    </div>
                </div>
                 <div class="flex items-start">
                    <span class="w-4 h-4 rounded-full mt-1 mr-3 flex-shrink-0" style="background-color: #5E7A4A;"></span>
                    <div>
                        <strong class="text-gray-700">Flexible Together Time:</strong>
                        <span class="text-gray-600 text-sm">Our casual time sharing the same space, including quiet nights, weekends, and travel between homes.</span>
                    </div>
                </div>
                 <div class="flex items-start">
                    <span class="w-4 h-4 rounded-full mt-1 mr-3 flex-shrink-0" style="background-color: #8A9A5B;"></span>
                    <div>
                        <strong class="text-sage">Social Time Together:</strong>
                        <span class="text-gray-600 text-sm">Time spent with friends and family as a couple, like watching games or group dinners.</span>
                    </div>
                </div>
                 <div class="flex items-start">
                    <span class="w-4 h-4 rounded-full mt-1 mr-3 flex-shrink-0" style="background-color: #EAD3A2;"></span>
                    <div>
                        <strong class="text-yellow-800">Apart:</strong>
                        <span class="text-gray-600 text-sm">Nights for solo work trips and separate boys/girls nights out.</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section: Next Steps & To-Dos -->
        <section id="todos" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-8">Next Steps & To-Dos</h2>
            <div id="todo-list" class="space-y-4 max-w-md mx-auto">
                <div class="flex items-center">
                    <input id="todo1" type="checkbox" class="h-5 w-5 rounded border-gray-300 text-navy focus:ring-navy cursor-pointer">
                    <label for="todo1" class="ml-3 text-gray-700 select-none cursor-pointer transition-all duration-200">Update Shared Calendar</label>
                </div>
                <div class="flex items-center">
                    <input id="todo2" type="checkbox" class="h-5 w-5 rounded border-gray-300 text-navy focus:ring-navy cursor-pointer">
                    <label for="todo2" class="ml-3 text-gray-700 select-none cursor-pointer transition-all duration-200">Decide on Wedding Scenario</label>
                </div>
                <!-- Gemini Feature: Getaway Planner -->
                <div id="getaway-todo-item">
                    <div class="flex items-center">
                        <input id="todo3" type="checkbox" class="h-5 w-5 rounded border-gray-300 text-navy focus:ring-navy cursor-pointer">
                        <label for="todo3" class="ml-3 text-gray-700 select-none cursor-pointer transition-all duration-200">Plan a romantic getaway</label>
                    </div>
                    <div id="getaway-planner" class="mt-4 ml-8 space-y-2">
                        <input type="text" id="getaway-prompt" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-navy focus:ring-navy sm:text-sm" placeholder="e.g., A cozy cabin weekend in the mountains">
                        <button id="get-getaway-btn" class="bg-sage text-white font-bold py-2 px-4 rounded-md hover:bg-sage/90 transition-colors w-full">✨ Get Getaway Ideas</button>
                        <div id="getaway-loader" class="hidden spinner"></div>
                        <div id="getaway-output" class="gemini-output hidden"></div>
                    </div>
                </div>
                <div class="flex items-center">
                    <input id="todo4" type="checkbox" class="h-5 w-5 rounded border-gray-300 text-navy focus:ring-navy cursor-pointer">
                    <label for="todo4" class="ml-3 text-gray-700 select-none cursor-pointer transition-all duration-200">Look at puppies</label>
                </div>
                <!-- Gemini Feature: Meal Planner -->
                <div id="meal-todo-item">
                    <div class="flex items-center">
                        <input id="todo5" type="checkbox" class="h-5 w-5 rounded border-gray-300 text-navy focus:ring-navy cursor-pointer">
                        <label for="todo5" class="ml-3 text-gray-700 select-none cursor-pointer transition-all duration-200">Pick meals for date nights</label>
                    </div>
                    <div id="meal-planner" class="mt-4 ml-8">
                         <button id="get-meals-btn" class="bg-sage text-white font-bold py-2 px-4 rounded-md hover:bg-sage/90 transition-colors w-full">✨ Suggest Meal Ideas</button>
                         <div id="meals-loader" class="hidden spinner"></div>
                         <div id="meals-output" class="gemini-output hidden"></div>
                    </div>
                </div>
            </div>
            <p class="text-xs text-center mt-6 text-gray-400">✨ AI features powered by Gemini</p>
        </section>

        <!-- Section: Spin the Wheel Decision Maker -->
        <section id="spinner" class="section-card">
            <h2 class="text-2xl font-bold text-center mb-1">Spin for Fun!</h2>
            <p class="text-center text-gray-500 mb-8">Can't decide on a date night? Let the wheel choose.</p>
            <div class="grid md:grid-cols-2 gap-8 items-start">
                <!-- Wheel Controls & Options -->
                <div>
                    <div class="bg-gray-50 p-4 rounded-lg mb-4">
                        <h3 class="font-bold text-lg mb-3 text-center">Add Your Choices</h3>
                        <div class="flex space-x-2">
                            <input type="text" id="optionInput" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-[#1A3A5A] focus:ring-[#1A3A5A] sm:text-sm" placeholder="e.g., Movie Night">
                            <button id="addOptionBtn" class="bg-navy text-white font-bold py-2 px-4 rounded-md hover:bg-navy/90 transition-colors flex-shrink-0">Add</button>
                        </div>
                        <p id="error-message" class="text-red-500 text-sm mt-2 text-center h-4"></p>
                    </div>
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <h3 class="font-bold text-lg mb-3 text-center">Current Options</h3>
                        <ul id="optionsList" class="space-y-2 text-sm max-h-48 overflow-y-auto">
                            <!-- Options will be dynamically added here -->
                        </ul>
                    </div>
                </div>
                <!-- Wheel Canvas -->
                <div class="flex flex-col items-center justify-center space-y-4">
                     <div class="relative">
                        <div class="pointer"></div>
                        <canvas id="wheelCanvas" width="500" height="500" class="max-w-xs w-full"></canvas>
                    </div>
                    <button id="spinBtn" class="bg-sage text-white text-xl font-bold py-3 px-10 rounded-full hover:bg-sage/90 transition-colors shadow-lg disabled:bg-gray-400 disabled:cursor-not-allowed">SPIN</button>
                </div>
            </div>
        </section>


        <!-- Footer -->
        <footer class="text-center mt-4 mb-8">
            <p class="text-lg text-navy font-semibold italic">"An amazing year of balance, adventure, and partnership ahead."</p>
        </footer>

    </div>

    <!-- Winner Modal from Spin the Wheel -->
    <div id="winnerModal" class="fixed inset-0 bg-black bg-opacity-60 items-center justify-center z-50 modal-hidden">
        <canvas id="confettiCanvas" class="absolute top-0 left-0 w-full h-full pointer-events-none"></canvas>
        <div id="modalContent" class="bg-white p-8 rounded-2xl shadow-xl text-center transform transition-all max-w-sm w-full mx-4">
            <p class="text-gray-500 text-lg">The winner is...</p>
            <h2 id="winnerText" class="text-4xl font-bold text-navy my-4 break-words"></h2>
            <div class="space-y-3 mt-6">
                <button id="removeWinnerBtn" class="bg-red-500 text-white font-bold py-2 px-6 rounded-lg w-full hover:bg-red-600 transition-colors">Remove & Spin Again</button>
                <button id="keepWinnerBtn" class="bg-gray-300 text-gray-800 font-bold py-2 px-6 rounded-lg w-full hover:bg-gray-400 transition-colors">Keep & Close</button>
            </div>
        </div>
    </div>


    <script>
        // --- Navigation Menu Logic ---
        const menuButton = document.getElementById('menu-button');
        const navMenu = document.getElementById('nav-menu');
        const pageOverlay = document.getElementById('page-overlay');
        const navLinks = document.querySelectorAll('.nav-link');

        function toggleMenu() {
            navMenu.classList.toggle('is-open');
            pageOverlay.classList.toggle('is-visible');
        }

        menuButton.addEventListener('click', toggleMenu);
        pageOverlay.addEventListener('click', toggleMenu);
        navLinks.forEach(link => {
            link.addEventListener('click', () => {
                if (navMenu.classList.contains('is-open')) {
                    toggleMenu();
                }
            });
        });

        // Chart.js Logic (from infographic)
        const ctx = document.getElementById('timeTogetherChart').getContext('2d');
        const flexSlider = document.getElementById('flex-slider');
        const flexNightsValue = document.getElementById('flex-nights-value');
        const tokenContainer = document.getElementById('token-container');
        const initialTokens = Array.from(tokenContainer.children);

        const initialData = {
            quality: 104,
            flexible: 144,
            social: 52,
            apart: 65,
        };
        const totalNights = 365;
        let chart;

        const chartConfig = {
            type: 'doughnut',
            data: {
                labels: [
                    'Dedicated Quality Time',
                    'Flexible Together Time',
                    'Social Time Together',
                    'Apart'
                ],
                datasets: [{
                    label: 'Nights',
                    data: [], // will be populated by updateChart
                    backgroundColor: [
                        '#1A3A5A', // Navy
                        '#5E7A4A', // Darker Sage
                        '#8A9A5B', // Sage
                        '#EAD3A2'  // Gold/Accent
                    ],
                    borderColor: '#FDFBF7',
                    borderWidth: 4,
                    hoverOffset: 10
                }]
            },
            options: {
                responsive: true,
                cutout: '65%',
                plugins: {
                    legend: {
                        display: false // Hides the default chart legend
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                const value = context.parsed;
                                const percentage = ((value / totalNights) * 100).toFixed(0);
                                label += `${value} nights (${percentage}%)`;
                                return label;
                            }
                        }
                    }
                }
            }
        };

        function updateChart() {
            const flexNights = parseInt(flexSlider.value, 10);
            flexNightsValue.textContent = flexNights;

            const tokensToShow = Math.ceil((1 - (flexNights / flexSlider.max)) * initialTokens.length);
             initialTokens.forEach((token, index) => {
                if (index < tokensToShow) {
                    token.style.opacity = '1';
                    token.style.transform = 'translateY(0)';
                } else {
                    token.style.opacity = '0';
                    token.style.transform = 'translateY(20px)';
                }
            });

            const currentData = { ...initialData };
            currentData.flexible = Math.max(0, initialData.flexible - flexNights);
            currentData.apart = initialData.apart + flexNights;

            const newData = [
                currentData.quality,
                currentData.flexible,
                currentData.social,
                currentData.apart
            ];

            if (chart) {
                chart.data.datasets[0].data = newData;
                chart.update();
            } else {
                chartConfig.data.datasets[0].data = newData;
                chart = new Chart(ctx, chartConfig);
            }
        }

        flexSlider.addEventListener('input', updateChart);
        updateChart();

        // To-Do List Logic
        const todoList = document.getElementById('todo-list');
        
        todoList.addEventListener('change', function(event) {
            if (event.target.type !== 'checkbox') return;

            const label = event.target.nextElementSibling;
            if (event.target.checked) {
                label.classList.add('line-through', 'text-gray-400');
            } else {
                label.classList.remove('line-through', 'text-gray-400');
            }
        });

        // Calendar Logic
        const addEventBtn = document.getElementById('add-event-btn');
        const calendarGrid = document.getElementById('calendar-grid');

        addEventBtn.addEventListener('click', () => {
            const eventNameInput = document.getElementById('event-name');
            const eventDaySelect = document.getElementById('event-day');
            const eventTypeSelect = document.getElementById('event-type');

            const eventName = eventNameInput.value.trim();
            const eventDay = eventDaySelect.value.toLowerCase();
            const eventType = eventTypeSelect.value;

            if (!eventName) {
                // Using a more subtle notification instead of alert()
                eventNameInput.classList.add('border-red-500');
                setTimeout(() => eventNameInput.classList.remove('border-red-500'), 2000);
                return;
            }

            const eventElement = document.createElement('div');
            eventElement.className = `calendar-event event-${eventType}`;
            
            const eventText = document.createElement('span');
            eventText.textContent = eventName;
            
            const removeBtn = document.createElement('span');
            removeBtn.className = 'remove-event';
            removeBtn.innerHTML = '&times;';
            
            eventElement.appendChild(eventText);
            eventElement.appendChild(removeBtn);

            const dayColumn = document.getElementById(`calendar-${eventDay}`).querySelector('.p-2');
            dayColumn.appendChild(eventElement);

            eventNameInput.value = '';
        });

        calendarGrid.addEventListener('click', function(e) {
            if (e.target.classList.contains('remove-event')) {
                e.target.parentElement.remove();
            }
        });

        // --- Gemini API Logic ---
        const apiKey = ""; // Leave blank, will be handled by the environment

        async function callGemini(systemPrompt, userQuery) {
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: {
                    parts: [{ text: systemPrompt }]
                },
            };

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    throw new Error(`API call failed with status: ${response.status}`);
                }

                const result = await response.json();
                const candidate = result.candidates?.[0];

                if (candidate && candidate.content?.parts?.[0]?.text) {
                    return candidate.content.parts[0].text;
                } else {
                    return "Sorry, I couldn't generate a response. Please try again.";
                }
            } catch (error) {
                console.error("Gemini API call error:", error);
                return "An error occurred while contacting the AI. Please check the console for details.";
            }
        }

        // Meal Planner Feature
        const getMealsBtn = document.getElementById('get-meals-btn');
        const mealsLoader = document.getElementById('meals-loader');
        const mealsOutput = document.getElementById('meals-output');

        getMealsBtn.addEventListener('click', async () => {
            mealsLoader.classList.remove('hidden');
            mealsOutput.classList.add('hidden');
            
            const systemPrompt = "You are a creative chef specializing in romantic and fun at-home date night meals. Provide 5 unique, creative, and delicious meal ideas for a couple to cook together. For each idea, provide a catchy name and a brief, enticing description. The meals should range in difficulty but be achievable for home cooks. Present the output as a numbered list with markdown for bolding the names.";
            const userQuery = "Suggest 5 date night meal ideas.";
            
            const responseText = await callGemini(systemPrompt, userQuery);
            
            mealsOutput.innerHTML = responseText.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>'); // Basic markdown for bold
            mealsLoader.classList.add('hidden');
            mealsOutput.classList.remove('hidden');
        });
        
        // Getaway Planner Feature
        const getGetawayBtn = document.getElementById('get-getaway-btn');
        const getawayLoader = document.getElementById('getaway-loader');
        const getawayOutput = document.getElementById('getaway-output');
        const getawayPromptInput = document.getElementById('getaway-prompt');

        getGetawayBtn.addEventListener('click', async () => {
            const userQuery = getawayPromptInput.value.trim();
            if (!userQuery) {
                getawayPromptInput.classList.add('border-red-500');
                setTimeout(() => getawayPromptInput.classList.remove('border-red-500'), 2000);
                return;
            }

            getawayLoader.classList.remove('hidden');
            getawayOutput.classList.add('hidden');

            const systemPrompt = "You are a helpful travel agent who specializes in romantic getaways for couples. Based on the user's input, suggest a detailed itinerary for a romantic getaway. The itinerary should include a destination, accommodation suggestions (style, not specific hotels), 3-4 activities per day, and dining recommendations (type of cuisine/vibe). The getaway should be for 3 days and 2 nights. Use markdown for headings and bold text.";
            
            const responseText = await callGemini(systemPrompt, userQuery);
            
            // Basic markdown processing
            let htmlResponse = responseText.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
            htmlResponse = htmlResponse.replace(/### (.*?)\n/g, '<h3 class="text-lg font-bold mt-4 mb-2">$1</h3>');
            htmlResponse = htmlResponse.replace(/## (.*?)\n/g, '<h2 class="text-xl font-bold mt-6 mb-3">$1</h2>');
            
            getawayOutput.innerHTML = htmlResponse;
            getawayLoader.classList.add('hidden');
            getawayOutput.classList.remove('hidden');
        });
        
        // --- Spin the Wheel Logic ---
        const wheelCanvas = document.getElementById('wheelCanvas');
        const wheelCtx = wheelCanvas.getContext('2d');
        const spinBtn = document.getElementById('spinBtn');
        const optionInput = document.getElementById('optionInput');
        const addOptionBtn = document.getElementById('addOptionBtn');
        const optionsList = document.getElementById('optionsList');
        const errorMessage = document.getElementById('error-message');
        const winnerModal = document.getElementById('winnerModal');
        const winnerText = document.getElementById('winnerText');
        const removeWinnerBtn = document.getElementById('removeWinnerBtn');
        const keepWinnerBtn = document.getElementById('keepWinnerBtn');
        const confettiCanvas = document.getElementById('confettiCanvas');
        const confettiCtx = confettiCanvas.getContext('2d');
        let confettiAnimationId;

        let wheelOptions = [];
        const wheelColors = ['#1A3A5A', '#8A9A5B', '#FDFBF7', '#EAD3A2', '#5E7A4A', '#b3cde0', '#6497b1', '#005b96', '#03396c', '#011f4b'];
        let startAngle = 0;
        let arc = 0;
        let spinTimeout = null;
        let spinAngleStart = 0;
        let spinTime = 0;
        let spinTimeTotal = 0;
        let isSpinning = false;

        function drawWheel() {
            const numOptions = wheelOptions.length;
            wheelCtx.clearRect(0, 0, wheelCanvas.width, wheelCanvas.height);

            if (numOptions === 0) {
                 wheelCtx.save();
                 wheelCtx.fillStyle = '#f3f4f6';
                 wheelCtx.beginPath();
                 wheelCtx.arc(250, 250, 250, 0, Math.PI * 2);
                 wheelCtx.fill();
                 wheelCtx.fillStyle = '#9ca3af';
                 wheelCtx.font = 'bold 20px Poppins, sans-serif';
                 wheelCtx.textAlign = 'center';
                 wheelCtx.fillText('Add options to spin!', 250, 250);
                 wheelCtx.restore();
                 return;
            }
            
            arc = Math.PI * 2 / numOptions;
            wheelCtx.strokeStyle = '#ccc';
            wheelCtx.lineWidth = 2;
            wheelCtx.font = 'bold 16px Poppins, sans-serif';

            for (let i = 0; i < numOptions; i++) {
                const angle = startAngle + i * arc;
                wheelCtx.fillStyle = wheelColors[i % wheelColors.length];
                wheelCtx.beginPath();
                wheelCtx.arc(250, 250, 250, angle, angle + arc, false);
                wheelCtx.arc(250, 250, 0, angle + arc, angle, true);
                wheelCtx.stroke();
                wheelCtx.fill();
                wheelCtx.save();
                wheelCtx.fillStyle = (i % 4 === 2) ? '#333' : 'white';
                wheelCtx.translate(250 + Math.cos(angle + arc / 2) * 180, 250 + Math.sin(angle + arc / 2) * 180);
                wheelCtx.rotate(angle + arc / 2 + Math.PI / 2);
                const text = wheelOptions[i];
                const maxTextWidth = 120;
                let displayText = text;
                if(wheelCtx.measureText(text).width > maxTextWidth) {
                    while(wheelCtx.measureText(displayText + '...').width > maxTextWidth && displayText.length > 0) {
                        displayText = displayText.slice(0, -1);
                    }
                    displayText += '...';
                }
                wheelCtx.fillText(displayText, -wheelCtx.measureText(displayText).width / 2, 0);
                wheelCtx.restore();
            }
        }
        
        function updateOptionsList() {
            optionsList.innerHTML = '';
            if (wheelOptions.length === 0) {
                 optionsList.innerHTML = '<li class="text-gray-400 text-center">No options yet!</li>';
            }
            wheelOptions.forEach((option, index) => {
                const li = document.createElement('li');
                li.className = 'flex justify-between items-center bg-gray-100 p-2 rounded-md';
                li.textContent = option;
                const removeBtn = document.createElement('button');
                removeBtn.innerHTML = '&times;';
                removeBtn.className = 'font-bold text-red-500 hover:text-red-700 ml-2';
                removeBtn.onclick = () => removeWheelOption(index);
                li.appendChild(removeBtn);
                optionsList.appendChild(li);
            });
            spinBtn.disabled = wheelOptions.length < 2;
        }

        function addWheelOption() {
            const newOption = optionInput.value.trim();
            errorMessage.textContent = '';
            if (newOption) {
                if (wheelOptions.length >= 10) {
                    errorMessage.textContent = 'Maximum of 10 options allowed.';
                    return;
                }
                wheelOptions.push(newOption);
                optionInput.value = '';
                updateOptionsList();
                drawWheel();
            }
        }
        
        function removeWheelOption(indexToRemove) {
            wheelOptions.splice(indexToRemove, 1);
            updateOptionsList();
            drawWheel();
        }

        function rotateWheel() {
            spinTime += 30;
            if (spinTime >= spinTimeTotal) {
                stopRotateWheel();
                return;
            }
            const spinAngle = spinAngleStart - easeOut(spinTime, 0, spinAngleStart, spinTimeTotal);
            startAngle += (spinAngle * Math.PI / 180);
            drawWheel();
            spinTimeout = requestAnimationFrame(rotateWheel);
        }

        function stopRotateWheel() {
            cancelAnimationFrame(spinTimeout);
            const degrees = startAngle * 180 / Math.PI + 90;
            const arcd = arc * 180 / Math.PI;
            const winnerIndex = Math.floor((360 - degrees % 360) / arcd);
            showWinnerModal(wheelOptions[winnerIndex], winnerIndex);
        }

        function easeOut(t, b, c, d) {
            const ts = (t /= d) * t;
            const tc = ts * t;
            return b + c * (tc + -3 * ts + 3 * t);
        }
        
        function spinWheel() {
            if (isSpinning || wheelOptions.length < 2) return;
            isSpinning = true;
            spinBtn.disabled = true;
            spinAngleStart = Math.random() * 10 + 10;
            spinTime = 0;
            spinTimeTotal = Math.random() * 3000 + 4000;
            rotateWheel();
        }
        
        function showWinnerModal(winner, index) {
            winnerText.textContent = winner;
            winnerModal.classList.remove('modal-hidden');
            winnerModal.classList.add('modal-visible');
            startConfetti();
            function handleRemove() { removeWheelOption(index); cleanup(); }
            function handleKeep() { cleanup(); }
            function cleanup() {
                winnerModal.classList.add('modal-hidden');
                winnerModal.classList.remove('modal-visible');
                isSpinning = false;
                spinBtn.disabled = wheelOptions.length < 2;
                stopConfetti();
                removeWinnerBtn.removeEventListener('click', handleRemove);
                keepWinnerBtn.removeEventListener('click', handleKeep);
            }
            removeWinnerBtn.addEventListener('click', handleRemove, { once: true });
            keepWinnerBtn.addEventListener('click', handleKeep, { once: true });
        }

        let particles = [];
        function startConfetti() {
            confettiCanvas.width = window.innerWidth;
            confettiCanvas.height = window.innerHeight;
            particles = [];
            for (let i = 0; i < 200; i++) { particles.push(new Particle()); }
            confettiLoop();
        }
        function stopConfetti() {
            particles = [];
            cancelAnimationFrame(confettiAnimationId);
        }
        function confettiLoop() {
            confettiAnimationId = requestAnimationFrame(confettiLoop);
            confettiCtx.clearRect(0, 0, confettiCanvas.width, confettiCanvas.height);
            particles.forEach((particle, index) => {
                particle.update();
                particle.draw();
                if (particle.y > confettiCanvas.height) particles.splice(index, 1);
            });
        }
        class Particle {
            constructor() {
                this.x = Math.random() * confettiCanvas.width;
                this.y = Math.random() * -confettiCanvas.height;
                this.size = Math.random() * 10 + 5;
                this.speed = Math.random() * 5 + 2;
                this.gravity = 0.1;
                this.color = wheelColors[Math.floor(Math.random() * wheelColors.length)];
                this.opacity = 1;
                this.angle = Math.random() * Math.PI * 2;
                this.spin = (Math.random() - 0.5) * 0.2;
            }
            update() {
                this.y += this.speed;
                this.speed += this.gravity;
                this.x += Math.sin(this.angle) * 2;
                this.angle += this.spin;
            }
            draw() {
                confettiCtx.save();
                confettiCtx.fillStyle = this.color;
                confettiCtx.globalAlpha = this.opacity;
                confettiCtx.beginPath();
                confettiCtx.rect(this.x, this.y, this.size, this.size);
                confettiCtx.fill();
                confettiCtx.restore();
            }
        }
        addOptionBtn.addEventListener('click', addWheelOption);
        optionInput.addEventListener('keypress', (e) => { if (e.key === 'Enter') addWheelOption(); });
        spinBtn.addEventListener('click', spinWheel);
        updateOptionsList();
        drawWheel();
    </script>
</body>
</html>







