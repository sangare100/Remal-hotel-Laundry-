<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Remal Hotel & Villas - Smart Laundry System</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <style>
        @media print {
            body { background: white; color: black; padding: 0; }
            #app-container { max-width: 100% !important; width: 100% !important; padding: 0 !important; margin: 0 !important; }
            .no-print { display: none !important; }
            .print-page { display: block !important; page-break-before: always; }
        }
    </style>
</head>
<body class="bg-slate-50 font-sans text-slate-800 pb-16 antialiased">

    <div class="max-w-7xl mx-auto p-2 sm:p-4 lg:p-6 min-h-screen flex flex-col" id="app-container">
        
        <div class="no-print flex flex-col sm:flex-row justify-between items-center gap-4 mb-6 bg-slate-900 p-4 rounded-2xl shadow-md border-b-2 border-[#e3b28d]">
            <div class="flex items-center gap-3">
                <img src="1000270338.jpg" alt="Remal Logo" class="h-12 w-auto object-contain">
                <div class="flex flex-col">
                    <span class="text-sm font-black uppercase tracking-widest text-white">REMAL</span>
                    <span class="text-[10px] uppercase tracking-wider text-slate-400 font-medium -mt-1">HOTEL & VILLAS</span>
                </div>
            </div>
            
            <select id="lang-select" class="w-full sm:w-auto bg-slate-800 text-white border border-slate-700 rounded-xl px-3 py-2.5 text-xs font-bold focus:outline-none focus:ring-1 focus:ring-[#e3b28d]">
                <option value="en" selected>🇬🇧 English</option>
                <option value="fr">🇫🇷 Français</option>
                <option value="hi">🇮🇳 हिन्दी (Hindi)</option>
                <option value="ar">🇦🇪 العربية (Arabic)</option>
                <option value="bn">🇧🇩 বাংলা (Bengali)</option>
            </select>
        </div>

        <header class="no-print bg-slate-900 text-white p-4 sm:p-6 rounded-2xl shadow-xl mb-6 flex flex-col sm:flex-row items-center justify-between gap-4">
            <div class="text-center sm:text-left">
                <h1 class="text-lg sm:text-xl font-bold tracking-wide" id="text-title">Morning Collection</h1>
                <p class="text-[10px] sm:text-xs text-slate-400" id="current-date">Date</p>
            </div>
            <div class="flex gap-2 w-full sm:w-auto justify-center">
                <div class="bg-slate-800 border border-[#e3b28d]/30 px-3 py-1.5 sm:px-4 sm:py-2 rounded-xl text-center flex-1 sm:flex-none min-w-[90px]">
                    <span class="block text-xl sm:text-2xl font-black text-[#e3b28d]" id="total-count">0</span>
                    <span class="text-[8px] sm:text-[9px] uppercase font-bold tracking-wider text-slate-400" id="text-rooms-unit">Bags Collected</span>
                </div>
                <div class="bg-slate-800 border border-teal-500/30 px-3 py-1.5 sm:px-4 sm:py-2 rounded-xl text-center flex-1 sm:flex-none min-w-[90px]">
                    <span class="block text-xl sm:text-2xl font-black text-teal-400" id="spa-total-count">0</span>
                    <span class="text-[8px] sm:text-[9px] uppercase font-bold tracking-wider text-slate-400" id="text-spa-unit">Spa Items</span>
                </div>
            </div>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 sm:gap-6 items-start">
            
            <div class="no-print lg:col-span-5 space-y-4 sm:space-y-6">
                
                <div class="bg-white p-4 sm:p-5 rounded-2xl shadow-xs border border-slate-100 space-y-4">
                    <div class="flex justify-between items-center border-b border-slate-100 pb-2">
                        <h2 class="text-xs font-bold text-slate-400 uppercase tracking-widest flex items-center gap-2">
                            <i class="fas fa-clipboard-check text-[#e3b28d]"></i>
                            <span id="text-register-title">Laundry Collection Form</span>
                        </h2>
                        <div class="text-right">
                            <span id="device-live-date" class="block text-[9px] font-bold text-slate-400 uppercase"></span>
                            <span id="device-live-time" class="text-[11px] font-black text-slate-700 bg-slate-100 px-2 py-0.5 rounded-md"></span>
                        </div>
                    </div>

                    <form id="laundry-form" class="space-y-4">
                        <div>
                            <label for="room-number" class="block text-xs font-bold text-slate-700 mb-1" id="text-room-label">Room Number</label>
                            <input type="number" id="room-number" placeholder="e.g. 105, 135, 224" required
                                class="w-full px-4 py-2.5 border border-slate-200 rounded-xl font-bold text-base focus:outline-none focus:ring-2 focus:ring-[#e3b28d]">
                            <p id="room-validation-msg" class="text-[10px] text-red-500 font-medium mt-1 hidden">⚠️ Room error</p>
                        </div>

                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1" id="text-status-label">Bag Status / Allowance</label>
                            <div class="grid grid-cols-2 gap-2">
                                <label class="border border-slate-200 rounded-xl p-2.5 flex flex-col items-center justify-center cursor-pointer bg-slate-50 text-xs font-bold">
                                    <input type="radio" name="status-type" value="3 Pcs Free" checked class="accent-slate-900 mb-0.5">
                                    <span class="text-emerald-700 text-center text-[11px] sm:text-xs">3 Pcs Free</span>
                                </label>
                                <label class="border border-slate-200 rounded-xl p-2.5 flex flex-col items-center justify-center cursor-pointer bg-slate-50 text-xs font-bold">
                                    <input type="radio" name="status-type" value="4 Pcs Free" class="accent-slate-900 mb-0.5">
                                    <span class="text-teal-700 text-center text-[11px] sm:text-xs">4 Pcs Free</span>
                                </label>
                                <label class="border border-slate-200 rounded-xl p-2.5 flex flex-col items-center justify-center cursor-pointer bg-slate-50 text-xs font-bold">
                                    <input type="radio" name="status-type" value="Chargeable" class="accent-slate-900 mb-0.5">
                                    <span class="text-amber-700 text-center text-[11px] sm:text-xs">Chargeable</span>
                                </label>
                                <label class="border border-slate-200 rounded-xl p-2.5 flex flex-col items-center justify-center cursor-pointer bg-slate-50 text-xs font-bold">
                                    <input type="radio" name="status-type" value="No Laundry" class="accent-slate-900 mb-0.5">
                                    <span class="text-slate-400 text-center text-[11px] sm:text-xs" id="label-no-laundry">No Laundry Bag</span>
                                </label>
                            </div>
                        </div>

                        <div id="clothes-counters-section" class="bg-slate-50 p-3 rounded-xl border border-slate-100 space-y-3">
                            <span class="block text-xs font-bold text-slate-500 uppercase tracking-wider" id="text-clothes-details">Clothes Details</span>
                            <div class="flex items-center justify-between">
                                <span class="text-xs font-medium text-slate-700" id="label-hanger">Hanger Clothes</span>
                                <div class="flex items-center gap-2">
                                    <button type="button" onclick="decrementCounter('hanger')" class="w-8 h-8 rounded-lg bg-white border border-slate-200 font-bold cursor-pointer">-</button>
                                    <span id="count-hanger" class="w-6 text-center font-bold">0</span>
                                    <button type="button" onclick="incrementCounter('hanger')" class="w-8 h-8 rounded-lg bg-white border border-slate-200 font-bold cursor-pointer">+</button>
                                </div>
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-xs font-medium text-slate-700" id="label-folding">Folding Clothes</span>
                                <div class="flex items-center gap-2">
                                    <button type="button" onclick="decrementCounter('folding')" class="w-8 h-8 rounded-lg bg-white border border-slate-200 font-bold cursor-pointer">-</button>
                                    <span id="count-folding" class="w-6 text-center font-bold">0</span>
                                    <button type="button" onclick="incrementCounter('folding')" class="w-8 h-8 rounded-lg bg-white border border-slate-200 font-bold cursor-pointer">+</button>
                                </div>
                            </div>
                            <div id="surplus-badge" class="hidden mt-2 p-2 rounded-lg bg-red-50 border border-red-200 text-red-700 font-bold text-center text-xs"></div>
                        </div>

                        <button type="submit" class="w-full bg-slate-900 text-[#e3b28d] font-bold py-3 rounded-xl shadow-md cursor-pointer text-sm">
                            <i class="fas fa-check-circle"></i> <span id="text-btn-add">Save Collection</span>
                        </button>
                    </form>
                </div>

                <div class="bg-teal-50/60 p-4 sm:p-5 rounded-2xl border border-teal-200 space-y-4">
                    <h2 class="text-xs font-bold text-teal-900 uppercase tracking-widest flex items-center gap-2">
                        <i class="fas fa-spa text-teal-600"></i>
                        <span id="text-spa-title">Spa Laundry Control</span>
                    </h2>
                    <form id="spa-form" class="space-y-4">
                        
                        <div>
                            <label for="spa-serial" class="block text-xs font-bold text-teal-950 mb-1" id="label-serial">Serial Number</label>
                            <input type="text" id="spa-serial" placeholder="e.g. SPA-042" required 
                                class="w-full px-3 py-2.5 bg-white border border-teal-200 rounded-xl font-bold text-sm focus:outline-none focus:ring-2 focus:ring-teal-600">
                        </div>

                        <div class="bg-white p-3 rounded-xl border border-teal-100 space-y-3">
                            <div class="flex items-center justify-between">
                                <div class="flex flex-col">
                                    <span class="text-xs font-medium text-slate-700" id="label-sheets">Bed Sheets</span>
                                    <span class="text-[10px] text-slate-400 font-medium">2 AED / pc</span>
                                </div>
                                <div class="flex items-center gap-3">
                                    <span id="cost-sheets" class="text-xs font-bold text-slate-500 bg-slate-50 px-2 py-1 rounded">0 AED</span>
                                    <div class="flex items-center gap-2">
                                        <button type="button" onclick="decrementSpa('sheets')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">-</button>
                                        <span id="count-sheets" class="w-6 text-center font-bold text-xs">0</span>
                                        <button type="button" onclick="incrementSpa('sheets')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">+</button>
                                    </div>
                                </div>
                            </div>
                            <div class="flex items-center justify-between">
                                <div class="flex flex-col">
                                    <span class="text-xs font-medium text-slate-700" id="label-towels">Bath Towels</span>
                                    <span class="text-[10px] text-slate-400 font-medium">2 AED / pc</span>
                                </div>
                                <div class="flex items-center gap-3">
                                    <span id="cost-towels" class="text-xs font-bold text-slate-500 bg-slate-50 px-2 py-1 rounded">0 AED</span>
                                    <div class="flex items-center gap-2">
                                        <button type="button" onclick="decrementSpa('towels')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">-</button>
                                        <span id="count-towels" class="w-6 text-center font-bold text-xs">0</span>
                                        <button type="button" onclick="incrementSpa('towels')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">+</button>
                                    </div>
                                </div>
                            </div>
                            <div class="flex items-center justify-between">
                                <div class="flex flex-col">
                                    <span class="text-xs font-medium text-slate-700" id="label-hand-towels">Hand Towels</span>
                                    <span class="text-[10px] text-slate-400 font-medium">1 AED / pc</span>
                                </div>
                                <div class="flex items-center gap-3">
                                    <span id="cost-hand-towels" class="text-xs font-bold text-slate-500 bg-slate-50 px-2 py-1 rounded">0 AED</span>
                                    <div class="flex items-center gap-2">
                                        <button type="button" onclick="decrementSpa('handTowels')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">-</button>
                                        <span id="count-hand-towels" class="w-6 text-center font-bold text-xs">0</span>
                                        <button type="button" onclick="incrementSpa('handTowels')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">+</button>
                                    </div>
                                </div>
                            </div>
                            <div class="flex items-center justify-between">
                                <div class="flex flex-col">
                                    <span class="text-xs font-medium text-slate-700" id="label-bathrobes">Bathrobes</span>
                                    <span class="text-[10px] text-slate-400 font-medium">2 AED / pc</span>
                                </div>
                                <div class="flex items-center gap-3">
                                    <span id="cost-bathrobes" class="text-xs font-bold text-slate-500 bg-slate-50 px-2 py-1 rounded">0 AED</span>
                                    <div class="flex items-center gap-2">
                                        <button type="button" onclick="decrementSpa('bathrobes')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">-</button>
                                        <span id="count-bathrobes" class="w-6 text-center font-bold text-xs">0</span>
                                        <button type="button" onclick="incrementSpa('bathrobes')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">+</button>
                                    </div>
                                </div>
                            </div>
                            <div class="flex items-center justify-between">
                                <div class="flex flex-col">
                                    <span class="text-xs font-medium text-slate-700" id="label-pillows">Pillow Cases</span>
                                    <span class="text-[10px] text-slate-400 font-medium">1 AED / pc</span>
                                </div>
                                <div class="flex items-center gap-3">
                                    <span id="cost-pillows" class="text-xs font-bold text-slate-500 bg-slate-50 px-2 py-1 rounded">0 AED</span>
                                    <div class="flex items-center gap-2">
                                        <button type="button" onclick="decrementSpa('pillows')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">-</button>
                                        <span id="count-pillows" class="w-6 text-center font-bold text-xs">0</span>
                                        <button type="button" onclick="incrementSpa('pillows')" class="w-7 h-7 rounded-lg bg-slate-100 font-bold cursor-pointer">+</button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="bg-teal-900 text-white p-3 rounded-xl flex justify-between items-center font-bold shadow-inner">
                            <span class="text-xs uppercase tracking-wider" id="label-spa-total-invoice">Spa Invoice Total:</span>
                            <span class="text-base font-black text-[#e3b28d]" id="spa-grand-total">0 AED</span>
                        </div>

                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-[10px] font-bold text-slate-600 mb-1" id="label-collected-by">Collected By</label>
                                <input type="text" id="spa-collected-by" required class="w-full px-3 py-2 bg-white border border-teal-200 rounded-xl text-xs">
                            </div>
                            <div>
                                <label class="block text-[10px] font-bold text-slate-600 mb-1" id="label-delivered-by">Delivered By</label>
                                <input type="text" id="spa-delivered-by" required class="w-full px-3 py-2 bg-white border border-teal-200 rounded-xl text-xs">
                            </div>
                        </div>

                        <button type="submit" class="w-full bg-teal-700 text-white font-bold py-2.5 rounded-xl text-xs cursor-pointer shadow-xs">
                            <i class="fas fa-save"></i> <span id="text-btn-save-spa">Save Spa Entry</span>
                        </button>
                    </form>
                </div>

                <div class="bg-blue-50/60 p-4 sm:p-5 rounded-2xl border border-blue-200/70 space-y-4">
                    <h2 class="text-xs font-bold text-blue-800 uppercase tracking-widest flex items-center gap-2">
                        <i class="fas fa-warehouse text-blue-600"></i>
                        <span id="text-store-title">Store (Check-out Rooms)</span>
                    </h2>
                    <form id="store-form" class="space-y-3">
                        <div class="grid grid-cols-2 gap-2">
                            <input type="number" id="store-room" placeholder="Room" required class="w-full px-2 py-2.5 bg-white border border-blue-200 rounded-xl text-xs font-bold">
                            <input type="date" id="store-date" required class="w-full px-2 py-2.5 bg-white border border-blue-200 rounded-xl text-xs">
                        </div>
                        <div class="flex flex-col sm:flex-row gap-2">
                            <input type="text" id="store-details" placeholder="Details" required class="flex-grow px-3 py-2.5 bg-white border border-blue-200 rounded-xl text-xs">
                            <button type="submit" class="bg-blue-600 text-white px-4 py-2.5 rounded-xl text-xs font-bold cursor-pointer w-full sm:w-auto" id="text-btn-keep">Keep</button>
                        </div>
                    </form>
                </div>
            </div>

            <div class="lg:col-span-7 space-y-4 sm:space-y-6">
                
                <div class="bg-slate-900 text-white p-4 sm:p-5 rounded-2xl shadow-md space-y-3">
                    <h3 class="text-xs font-bold text-[#e3b28d] uppercase tracking-widest flex items-center gap-2">
                        <i class="fas fa-search"></i>
                        <span id="text-search-title">Search Archives (History)</span>
                    </h3>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <input type="text" id="search-room" placeholder="Room, Staff or S/N" class="bg-slate-800 border border-slate-700 text-white rounded-xl px-3 py-2.5 text-xs focus:outline-none focus:border-[#e3b28d]">
                        <input type="date" id="search-date" class="bg-slate-800 border border-slate-700 text-white rounded-xl px-3 py-2.5 text-xs focus:outline-none focus:border-[#e3b28d]">
                        <select id="search-type" class="bg-slate-800 border border-slate-700 text-white rounded-xl px-3 py-2.5 text-xs focus:outline-none">
                            <option value="all">All Records</option>
                            <option value="rooms">Rooms Only</option>
                            <option value="spa">Spa Only</option>
                        </select>
                    </div>

                    <button id="btn-print-pdf" onclick="generateA4Report()" class="hidden w-full mt-2 bg-blue-600 hover:bg-blue-700 text-white font-bold py-2.5 rounded-xl text-xs cursor-pointer shadow-xs items-center justify-center gap-2">
                        <i class="fas fa-print"></i> <span id="text-btn-print">Generate A4 PDF Report</span>
                    </button>

                    <div id="search-results" class="max-h-56 overflow-y-auto space-y-1.5 pt-2 hidden"></div>
                </div>

                <div class="bg-white p-4 sm:p-5 rounded-2xl shadow-xs border border-teal-100">
                    <h3 class="text-xs font-bold text-teal-700 uppercase tracking-widest mb-3" id="text-live-spa">Live Spa Daily Sheet</h3>
                    <ul id="spa-list" class="divide-y divide-teal-50 max-h-40 overflow-y-auto"></ul>
                </div>

                <div class="bg-white p-4 sm:p-5 rounded-2xl shadow-xs border border-slate-100">
                    <h3 class="text-xs font-bold text-blue-500 uppercase tracking-widest mb-3" id="text-live-store">Live Store Status</h3>
                    <ul id="store-list" class="space-y-2 max-h-40 overflow-y-auto"></ul>
                </div>

                <div class="bg-white p-4 sm:p-5 rounded-2xl shadow-xs border border-slate-100">
                    <div class="flex justify-between items-center mb-3">
                        <h3 class="text-xs font-bold text-slate-400 uppercase tracking-widest" id="text-history-title">Morning Sheet Status</h3>
                        <button id="clear-all" class="text-xs text-red-500 font-medium cursor-pointer"><i class="fas fa-archive"></i> <span id="text-btn-clear">Reset Shift</span></button>
                    </div>
                    <div id="empty-state" class="text-center py-6 text-slate-400 text-sm">No rooms collected yet.</div>
                    <ul id="laundry-list" class="divide-y divide-slate-100 max-h-72 overflow-y-auto"></ul>
                </div>
            </div>
        </div>

        <footer class="no-print mt-6">
            <button id="whatsapp-btn" class="w-full bg-[#25d366] text-white font-black py-4 rounded-xl shadow-md flex items-center justify-center gap-2 uppercase text-xs tracking-wider cursor-pointer">
                <i class="fab fa-whatsapp text-lg"></i> <span id="text-btn-wa">Send Summary to WhatsApp</span>
            </button>
        </footer>
    </div>

    <div id="a4-printable-area" class="hidden bg-white p-8 text-black max-w-[210mm] mx-auto">
        <div class="flex justify-between items-center border-b-4 border-slate-900 pb-4 mb-6">
            <div>
                <h1 class="text-2xl font-black uppercase tracking-widest">REMAL HOTEL & VILLAS</h1>
                <p class="text-xs uppercase tracking-wider text-slate-500 font-bold">Official Laundry & Spa Report</p>
            </div>
            <div class="text-right">
                <h2 class="text-sm font-black uppercase bg-slate-900 text-white px-3 py-1 rounded" id="pdf-report-date">DATE</h2>
            </div>
        </div>

        <div class="mb-8">
            <h3 class="text-xs font-bold uppercase tracking-widest bg-slate-100 p-2 border-l-4 border-slate-900 text-slate-800 mb-3" id="pdf-title-rooms">Rooms Laundry Collection</h3>
            <table class="w-full text-left text-xs border-collapse">
                <thead>
                    <tr class="border-b-2 border-slate-300 text-slate-500 font-bold">
                        <th class="py-2">Room</th>
                        <th class="py-2">Status / Allowance</th>
                        <th class="py-2">Hanger</th>
                        <th class="py-2">Folding</th>
                        <th class="py-2 text-right">Extra (Chargeable)</th>
                    </tr>
                </thead>
                <tbody id="pdf-rooms-tbody" class="divide-y divide-slate-200"></tbody>
            </table>
        </div>

        <div>
            <h3 class="text-xs font-bold uppercase tracking-widest bg-teal-50 p-2 border-l-4 border-teal-700 text-teal-900 mb-3" id="pdf-title-spa">Spa Laundry Collection</h3>
            <table class="w-full text-left text-[10px] border-collapse">
                <thead>
                    <tr class="border-b-2 border-teal-300 text-teal-800 font-bold">
                        <th class="py-2">S/N</th>
                        <th class="py-2">Time</th>
                        <th class="py-2">Sheets</th>
                        <th class="py-2">Towels</th>
                        <th class="py-2">Hand Twl</th>
                        <th class="py-2">Bathrobes</th>
                        <th class="py-2">Pillows</th>
                        <th class="py-2">Staff Details</th>
                        <th class="py-2 text-right">Total Invoice</th>
                    </tr>
                </thead>
                <tbody id="pdf-spa-tbody" class="divide-y divide-slate-200"></tbody>
            </table>
        </div>
    </div>

    <script>
        const channelKey = "remal_villas_laundry_spa_pricing_v13";

        const allValidRooms = [
            101,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,119,120,121,122,
            123,124,125,126,127,128,129,130,131,132,133,134,135,136,137,138,139,140,141,142,143,144,
            201,202,203,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,221,222,
            223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,238,239,240,241,242,243,244,245,246,
            301,302,303,304,305,306,307,308,309,310,311,312,313,314,315,316,317,318,319,320,321,322,323,324,
            325,326,327,328,329,330,331,332,333,334,335,336,337,338,339,340,341,342,343,344,345,346,347,348,
            401,402,403,404,405,406,407,408,409,410,411,412,413,414,415,416,417,418,419,420,421,422,423,424,
            425,426,427,428,429,430,431,432,433,434,435,436,437,438,439,440,441,442,443,444,445,446,447,448,
            501,502,503,504,505,506,507,508,509,510,511,512,513,514,515,516,517,518,519,520
        ];

        function checkRoomValidity(roomNum) { return allValidRooms.includes(parseInt(roomNum)); }

        const translations = {
            en: {
                title: "Morning Collection", roomsUnit: "Bags Saved", registerTitle: "Laundry Collection Form",
                roomLabel: "Room Number", statusLabel: "Bag Status / Allowance", clothesDetails: "Clothes Details",
                labelHanger: "Hanger Clothes", labelFolding: "Folding Clothes", labelNoLaundry: "No Laundry Bag",
                btnAdd: "Save Collection", historyTitle: "Morning Sheet Status", btnClear: "Archive Shift",
                errorMsg: "⚠️ Invalid Room Number", btnWa: "Send Summary to WhatsApp", emptyState: "No rooms collected yet.",
                storeTitle: "Store (Check-out Rooms)", btnKeep: "Keep", liveStore: "Live Store Status",
                searchTitle: "Search Archives (History)", confirmArchive: "Archive the current shift into permanent history?",
                confirmRemoveStore: "Remove from Store?", searchNoResult: "No past laundry record found.",
                placeholderRoom: "Room Number", placeholderDetails: "Details", alertInvalid: "Invalid room number!", surplusAlert: "Extra Pieces to Charge",
                textSpaTitle: "Spa Laundry Control", labelSheets: "Bed Sheets", labelTowels: "Bath Towels", labelHandTowels: "Hand Towels", labelBathrobes: "Bathrobes", labelPillows: "Pillow Cases",
                labelCollectedBy: "Collected By", labelDeliveredBy: "Delivered By", textBtnSaveSpa: "Save Spa Entry",
                textLiveSpa: "Live Spa Daily Sheet", textSpaUnit: "Spa Items", placeholderSearch: "Room, Staff or S/N",
                textBtnPrint: "Generate A4 PDF Report", labelSerial: "Serial Number", labelSpaInvoice: "Spa Invoice Total:"
            },
            fr: {
                title: "Collecte du Matin", roomsUnit: "Sacs Enregistrés", registerTitle: "Formulaire de Collecte Laundry",
                roomLabel: "Numéro de Chambre", statusLabel: "Statut du Sac / Quota", clothesDetails: "Détails des Vêtements",
                labelHanger: "Vêtements Cintre", labelFolding: "Vêtements Pliés", labelNoLaundry: "Pas de Sac Laundry",
                btnAdd: "Sauvegarder la Collecte", historyTitle: "Sujet de la Feuille du Matin", btnClear: "Archiver le Shift",
                errorMsg: "⚠️ Numéro de chambre invalide", btnWa: "Envoyer le résumé sur WhatsApp", emptyState: "Aucune chambre collectée pour le moment.",
                storeTitle: "Magasin (Chambres Check-out)", btnKeep: "Garder", liveStore: "Statut du Magasin en Direct",
                searchTitle: "Rechercher dans les Archives (Historique)", confirmArchive: "Archiver le shift actuel dans l'historique permanent ?",
                confirmRemoveStore: "Retirer du magasin ?", searchNoResult: "Aucun historique de blanchisserie trouvé.",
                placeholderRoom: "Numéro de chambre", placeholderDetails: "Détails", alertInvalid: "Numéro de chambre invalide !", surplusAlert: "Pièces en surplus à facturer",
                textSpaTitle: "Contrôle Blanchisserie du Spa", labelSheets: "Draps de Lit", labelTowels: "Serviettes Bain", labelHandTowels: "Serviettes Mains", labelBathrobes: "Peignoirs", labelPillows: "Taies d'Oreiller",
                labelCollectedBy: "Collecté Par", labelDeliveredBy: "Livré Par", textBtnSaveSpa:
