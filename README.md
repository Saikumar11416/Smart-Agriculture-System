<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Agriculture and Crop Management System</title>

<!-- Chart.js -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
 font-family:Arial,sans-serif;
 color:#fff;
 min-height:100vh;
 background:#173b20;
}

/* FARM BACKGROUND IMAGE */
body::before{
 content:"";
 position:fixed;
 inset:0;
 z-index:-2;
 background-image:url("https://images.unsplash.com/photo-1500382017468-9049fed747ef?auto=format&fit=crop&w=2000&q=90");
 background-size:cover;
 background-position:center;
 background-repeat:no-repeat;
}

/* LIGHT DARK OVERLAY - IMAGE WILL BE VISIBLE */
body::after{
 content:"";
 position:fixed;
 inset:0;
 z-index:-1;
 background:rgba(0,25,5,.28);
 pointer-events:none;
}

.app{display:flex;min-height:100vh}

/* SIDEBAR */
.sidebar{
 width:255px;
 min-width:255px;
 background:rgba(8,35,17,.90);
 backdrop-filter:blur(12px);
 padding:22px 14px;
 position:fixed;
 height:100vh;
 overflow-y:auto;
 border-right:1px solid rgba(255,255,255,.2);
}
.logo{
 font-size:21px;
 font-weight:bold;
 color:#b8ff9b;
 text-align:center;
 margin-bottom:8px;
}
.logo-sub{
 text-align:center;
 color:#ddd;
 font-size:12px;
 margin-bottom:25px;
}
.nav-btn{
 display:block;
 width:100%;
 padding:12px;
 margin:5px 0;
 border:0;
 border-radius:9px;
 background:transparent;
 color:white;
 text-align:left;
 font-size:14px;
 cursor:pointer;
 transition:.2s;
}
.nav-btn:hover,.nav-btn.active{
 background:#4c9b42;
 color:white;
}

/* MAIN CONTENT */
.main{
 margin-left:255px;
 width:calc(100% - 255px);
 padding:24px;
}
.topbar{
 display:flex;
 justify-content:space-between;
 align-items:center;
 gap:12px;
 flex-wrap:wrap;
 background:rgba(8,35,17,.75);
 padding:17px 20px;
 border-radius:14px;
 backdrop-filter:blur(8px);
 margin-bottom:22px;
 border:1px solid rgba(255,255,255,.15);
}
.topbar h1{font-size:23px;color:#eaffdf}
.topbar p{font-size:12px;color:#ddd;margin-top:5px}
.date{font-size:13px;color:#fff}

/* PAGES */
.page{display:none}
.page.active{display:block}
.page-heading{
 font-size:24px;
 margin-bottom:18px;
 color:#efffe9;
 text-shadow:0 2px 5px #18351b;
}
.description{
 color:#f1f1f1;
 margin-bottom:18px;
 line-height:1.5;
}

/* CARDS */
.cards{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(175px,1fr));
 gap:15px;
 margin-bottom:20px;
}
.card{
 background:rgba(9,38,18,.82);
 backdrop-filter:blur(9px);
 border:1px solid rgba(255,255,255,.2);
 border-radius:13px;
 padding:19px;
 box-shadow:0 5px 18px rgba(0,0,0,.16);
}
.card h3{font-size:13px;color:#d7f5d0;margin-bottom:12px}
.card .number{font-size:27px;font-weight:bold;color:#b7ff9e}
.card p{font-size:12px;color:#ddd;margin-top:8px}
.card-icon{font-size:25px;margin-bottom:10px}

/* PANELS */
.panel{
 background:rgba(8,35,17,.84);
 backdrop-filter:blur(10px);
 padding:20px;
 border-radius:13px;
 border:1px solid rgba(255,255,255,.2);
 margin-bottom:20px;
}
.panel h3{margin-bottom:15px;color:#c5ffb2}
.two-columns{
 display:grid;
 grid-template-columns:1fr 1fr;
 gap:18px;
}

/* CHARTS */
.chart-box{
 width:100%;
 height:260px;
 position:relative;
}
.small-chart{
 max-width:280px;
 height:210px;
 margin:auto;
 position:relative;
}

/* FORMS */
.form-grid{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
 gap:12px;
 margin-bottom:14px;
}
input,select,textarea{
 width:100%;
 padding:11px;
 border:1px solid #b5d7aa;
 border-radius:7px;
 margin:5px 0;
 background:#fff;
 color:#222;
 font-size:14px;
}
label{font-size:13px;color:#eaffdf}
button{
 cursor:pointer;
}
.btn{
 background:#58a946;
 color:white;
 border:0;
 padding:11px 17px;
 border-radius:7px;
 font-weight:bold;
 margin:5px 3px 5px 0;
}
.btn:hover{background:#347b2b}
.btn-red{background:#c94b42}
.btn-blue{background:#2879b9}
.btn-orange{background:#d58b25}
.btn-gray{background:#65736a}

/* TABLE */
.table-wrap{overflow-x:auto}
table{
 width:100%;
 border-collapse:collapse;
 min-width:600px;
}
th,td{
 padding:12px;
 border-bottom:1px solid rgba(255,255,255,.18);
 text-align:left;
 font-size:13px;
}
th{background:rgba(68,139,55,.65);color:white}
td{color:#fff}
tr:hover{background:rgba(255,255,255,.08)}

/* STATUS */
.status{
 display:inline-block;
 padding:5px 9px;
 border-radius:20px;
 background:#337b3c;
 font-size:11px;
}
.alert{
 padding:12px;
 background:rgba(201,139,30,.25);
 border-left:4px solid #ffc34c;
 border-radius:7px;
 margin:10px 0;
 font-size:13px;
}
.success{
 padding:12px;
 background:rgba(52,150,69,.25);
 border-left:4px solid #7bea75;
 border-radius:7px;
 margin:10px 0;
 font-size:13px;
}
.result{
 margin-top:15px;
 padding:15px;
 border-radius:8px;
 background:rgba(255,255,255,.12);
 line-height:1.7;
}
.footer{
 text-align:center;
 color:#eee;
 padding:20px;
 font-size:12px;
}
@media(max-width:850px){
 .sidebar{width:190px;min-width:190px}
 .main{margin-left:190px;width:calc(100% - 190px);padding:15px}
 .two-columns{grid-template-columns:1fr}
}
@media(max-width:600px){
 .app{display:block}
 .sidebar{
  position:relative;
  width:100%;
  min-width:0;
  height:auto;
  max-height:260px;
 }
 .main{margin:0;width:100%;padding:12px}
 .topbar h1{font-size:18px}
}
</style>
</head>

<body>
<div class="app">

<!-- SIDEBAR -->
<aside class="sidebar">
 <div class="logo">🌱 SMART AGRI</div>
 <div class="logo-sub">Agriculture & Crop Management</div>

 <button class="nav-btn active" onclick="showPage('dashboard',this)">🏠 Dashboard</button>
 <button class="nav-btn" onclick="showPage('farm',this)">🚜 Farm Management</button>
 <button class="nav-btn" onclick="showPage('crops',this)">🌾 Crop Management</button>
 <button class="nav-btn" onclick="showPage('recommend',this)">🧠 Crop Recommendation</button>
 <button class="nav-btn" onclick="showPage('irrigation',this)">💧 Irrigation System</button>
 <button class="nav-btn" onclick="showPage('soil',this)">🌍 Soil Monitoring</button>
 <button class="nav-btn" onclick="showPage('weather',this)">🌤 Weather Information</button>
 <button class="nav-btn" onclick="showPage('fertilizer',this)">🧪 Fertilizer Schedule</button>
 <button class="nav-btn" onclick="showPage('pest',this)">🐛 Pest Monitoring</button>
 <button class="nav-btn" onclick="showPage('tasks',this)">📋 Farm Task Planner</button>
 <button class="nav-btn" onclick="showPage('seeds',this)">🌱 Seed Inventory</button>
 <button class="nav-btn" onclick="showPage('economics',this)">💰 Farm Economics</button>
 <button class="nav-btn" onclick="showPage('reports',this)">📊 Reports</button>
 <button class="nav-btn" onclick="showPage('notifications',this)">🔔 Notifications</button>
</aside>

<!-- MAIN -->
<main class="main">

<div class="topbar">
 <div>
  <h1>Smart Agriculture System</h1>
  <p>Smart Farming | Crop Planning | Farm Monitoring</p>
 </div>
 <div class="date" id="todayDate"></div>
</div>

<!-- DASHBOARD -->
<section id="dashboard" class="page active">
 <h2 class="page-heading">🌿 Farm Dashboard</h2>
 <p class="description">Welcome to your Smart Agriculture and Crop Management Dashboard.</p>

 <div class="cards">
  <div class="card"><div class="card-icon">🚜</div><h3>Total Farm Area</h3><div class="number" id="farmAreaDisplay">10 Acres</div><p>Registered farm land</p></div>
  <div class="card"><div class="card-icon">🌾</div><h3>Total Crops</h3><div class="number" id="cropCount">4</div><p>Currently managed crops</p></div>
  <div class="card"><div class="card-icon">💧</div><h3>Water Usage</h3><div class="number" id="waterDisplay">450 L</div><p>Estimated daily usage</p></div>
  <div class="card"><div class="card-icon">🌍</div><h3>Soil Moisture</h3><div class="number" id="moistureDisplay">65%</div><p>Sample soil reading</p></div>
  <div class="card"><div class="card-icon">💰</div><h3>Estimated Income</h3><div class="number" id="incomeDisplay">₹85,000</div><p>Illustrative estimate</p></div>
  <div class="card"><div class="card-icon">🔔</div><h3>Farm Alerts</h3><div class="number" id="alertCount">2</div><p>Sample notifications</p></div>
 </div>

 <div class="two-columns">
  <div class="panel">
   <h3>📈 Weekly Water Usage</h3>
   <div class="chart-box"><canvas id="waterChart"></canvas></div>
  </div>
  <div class="panel">
   <h3>🌱 Crop Distribution</h3>
   <div class="small-chart"><canvas id="cropChart"></canvas></div>
  </div>
 </div>

 <div class="panel">
  <h3>⚠️ Farm Alerts</h3>
  <div class="alert">Soil moisture is a sample reading. Check field conditions regularly.</div>
  <div class="alert">Review fertilizer and irrigation schedules for your crops.</div>
 </div>
</section>

<!-- FARM MANAGEMENT -->
<section id="farm" class="page">
 <h2 class="page-heading">🚜 Farm Management</h2>
 <div class="panel">
  <h3>Enter Farm Details</h3>
  <div class="form-grid">
   <div><label>Farm Name</label><input id="farmName" placeholder="Enter farm name"></div>
   <div><label>Owner Name</label><input id="ownerName" placeholder="Enter owner name"></div>
   <div><label>Total Farm Area (Acres)</label><input type="number" id="farmArea" value="10"></div>
   <div><label>Location</label><input id="farmLocation" placeholder="Enter village / location"></div>
   <div><label>Soil Type</label><select id="farmSoil"><option>Black Soil</option><option>Red Soil</option><option>Alluvial Soil</option><option>Clay Soil</option><option>Sandy Soil</option></select></div>
   <div><label>Water Source</label><select id="waterSource"><option>Borewell</option><option>Canal</option><option>Rainwater</option><option>River</option><option>Other</option></select></div>
  </div>
  <button class="btn" onclick="saveFarm()">Save Farm Details</button>
  <div id="farmResult"></div>
 </div>
 <div class="panel">
  <h3>Farm Information</h3>
  <p id="farmInfo">Farm area: 10 Acres | Soil: Black Soil</p>
 </div>
</section>

<!-- CROP MANAGEMENT -->
<section id="crops" class="page">
 <h2 class="page-heading">🌾 Crop Management</h2>
 <div class="panel">
  <h3>Add New Crop</h3>
  <div class="form-grid">
   <div><label>Crop Name</label><input id="cropName" placeholder="Example: Paddy"></div>
   <div><label>Area (Acres)</label><input type="number" id="cropArea" placeholder="Enter area"></div>
   <div><label>Sowing Date</label><input type="date" id="sowingDate"></div>
   <div><label>Expected Harvest</label><input type="date" id="harvestDate"></div>
  </div>
  <button class="btn" onclick="addCrop()">Add Crop</button>
 </div>

 <div class="panel">
  <h3>Crop List</h3>
  <input id="cropSearch" placeholder="Search crop..." oninput="searchCrops()">
  <div class="table-wrap">
   <table id="cropTable">
    <thead><tr><th>Crop Name</th><th>Area</th><th>Sowing Date</th><th>Harvest Date</th><th>Status</th><th>Action</th></tr></thead>
    <tbody>
     <tr><td>Paddy</td><td>3</td><td>2026-06-01</td><td>2026-10-01</td><td><span class="status">Growing</span></td><td><button class="btn btn-red" onclick="deleteCrop(this)">Delete</button></td></tr>
     <tr><td>Wheat</td><td>2</td><td>2026-07-01</td><td>2026-11-01</td><td><span class="status">Growing</span></td><td><button class="btn btn-red" onclick="deleteCrop(this)">Delete</button></td></tr>
     <tr><td>Cotton</td><td>3</td><td>2026-06-15</td><td>2026-12-01</td><td><span class="status">Growing</span></td><td><button class="btn btn-red" onclick="deleteCrop(this)">Delete</button></td></tr>
     <tr><td>Maize</td><td>2</td><td>2026-07-10</td><td>2026-11-20</td><td><span class="status">Growing</span></td><td><button class="btn btn-red" onclick="deleteCrop(this)">Delete</button></td></tr>
    </tbody>
   </table>
  </div>
 </div>
</section>

<!-- CROP RECOMMENDATION -->
<section id="recommend" class="page">
 <h2 class="page-heading">🧠 Crop Recommendation</h2>
 <div class="panel">
  <h3>Smart Crop Suggestion</h3>
  <p class="description">Enter your field conditions to view a basic sample crop suggestion.</p>
  <div class="form-grid">
   <div><label>Soil Type</label><select id="recSoil"><option>Black Soil</option><option>Red Soil</option><option>Alluvial Soil</option><option>Sandy Soil</option></select></div>
   <div><label>Season</label><select id="recSeason"><option>Kharif</option><option>Rabi</option><option>Summer</option></select></div>
   <div><label>Water Availability</label><select id="recWater"><option>High</option><option>Medium</option><option>Low</option></select></div>
  </div>
  <button class="btn" onclick="recommendCrop()">Get Crop Recommendation</button>
  <div class="result" id="recommendResult">Your crop recommendation will appear here.</div>
 </div>
</section>

<!-- IRRIGATION -->
<section id="irrigation" class="page">
 <h2 class="page-heading">💧 Smart Irrigation System</h2>
 <div class="cards">
  <div class="card"><h3>Pump Status</h3><div class="number" id="pumpStatus">OFF</div></div>
  <div class="card"><h3>Soil Moisture</h3><div class="number" id="irrigationMoisture">65%</div></div>
  <div class="card"><h3>Water Usage</h3><div class="number" id="irrigationWater">450 L</div></div>
 </div>
 <div class="panel">
  <h3>Pump Control</h3>
  <p class="description">Demo control only. This does not connect to a real pump.</p>
  <button class="btn" onclick="pumpOn()">Turn Pump ON</button>
  <button class="btn btn-red" onclick="pumpOff()">Turn Pump OFF</button>
  <button class="btn btn-blue" onclick="autoIrrigation()">Automatic Irrigation Demo</button>
  <div class="result" id="pumpMessage">Pump is currently OFF.</div>
 </div>
</section>

<!-- SOIL -->
<section id="soil" class="page">
 <h2 class="page-heading">🌍 Soil Monitoring</h2>
 <div class="panel">
  <h3>Soil Parameters</h3>
  <div class="form-grid">
   <div><label>Soil Moisture (%)</label><input type="number" id="moistureInput" value="65" min="0" max="100"></div>
   <div><label>Soil pH</label><input type="number" id="soilPH" value="6.5" min="0" max="14" step="0.1"></div>
   <div><label>Temperature (°C)</label><input type="number" id="soilTemp" value="28"></div>
   <div><label>Nitrogen Level</label><select id="nitrogen"><option>Low</option><option selected>Medium</option><option>High</option></select></div>
  </div>
  <button class="btn" onclick="updateSoil()">Update Soil Data</button>
  <div class="result" id="soilResult">Sample soil readings are displayed.</div>
 </div>
</section>

<!-- WEATHER -->
<section id="weather" class="page">
 <h2 class="page-heading">🌤 Weather Information</h2>
 <div class="cards">
  <div class="card"><div class="card-icon">🌡️</div><h3>Temperature</h3><div class="number">29°C</div></div>
  <div class="card"><div class="card-icon">💧</div><h3>Humidity</h3><div class="number">68%</div></div>
  <div class="card"><div class="card-icon">🌧️</div><h3>Rainfall</h3><div class="number">12 mm</div></div>
  <div class="card"><div class="card-icon">💨</div><h3>Wind Speed</h3><div class="number">10 km/h</div></div>
 </div>
 <div class="panel">
  <h3>Weather Advisory</h3>
  <div class="success">Sample advisory: Check local weather forecasts before irrigation, spraying, or harvesting.</div>
  <p class="description">These are demonstration values, not live weather information.</p>
 </div>
</section>

<!-- FERTILIZER -->
<section id="fertilizer" class="page">
 <h2 class="page-heading">🧪 Fertilizer Schedule</h2>
 <div class="panel">
  <h3>Add Fertilizer Schedule</h3>
  <div class="form-grid">
   <div><label>Crop Name</label><input id="fertCrop" placeholder="Enter crop"></div>
   <div><label>Fertilizer Name</label><input id="fertName" placeholder="Enter fertilizer"></div>
   <div><label>Application Date</label><input type="date" id="fertDate"></div>
   <div><label>Quantity</label><input id="fertQty" placeholder="Example: 25 kg"></div>
  </div>
  <button class="btn" onclick="addFertilizer()">Add Schedule</button>
 </div>
 <div class="panel">
  <h3>Fertilizer Records</h3>
  <div class="table-wrap">
   <table id="fertTable">
    <thead><tr><th>Crop</th><th>Fertilizer</th><th>Date</th><th>Quantity</th><th>Action</th></tr></thead>
    <tbody></tbody>
   </table>
  </div>
 </div>
</section>

<!-- PEST -->
<section id="pest" class="page">
 <h2 class="page-heading">🐛 Pest Monitoring</h2>
 <div class="panel">
  <h3>Add Crop Health Observation</h3>
  <div class="form-grid">
   <div><label>Crop Name</label><input id="pestCrop" placeholder="Enter crop"></div>
   <div><label>Observation</label><input id="pestName" placeholder="Describe observation"></div>
   <div><label>Severity</label><select id="pestSeverity"><option>Low</option><option>Medium</option><option>High</option></select></div>
   <div><label>Date</label><input type="date" id="pestDate"></div>
  </div>
  <button class="btn" onclick="addPest()">Add Observation</button>
 </div>
 <div class="panel">
  <h3>Crop Health Records</h3>
  <div class="table-wrap">
   <table id="pestTable">
    <thead><tr><th>Crop</th><th>Observation</th><th>Severity</th><th>Date</th><th>Action</th></tr></thead>
    <tbody></tbody>
   </table>
  </div>
 </div>
</section>

<!-- TASKS -->
<section id="tasks" class="page">
 <h2 class="page-heading">📋 Farm Task Planner</h2>
 <div class="panel">
  <h3>Create Farm Task</h3>
  <div class="form-grid">
   <div><label>Task Name</label><input id="taskName" placeholder="Example: Watering"></div>
   <div><label>Due Date</label><input type="date" id="taskDate"></div>
   <div><label>Assigned Person</label><input id="taskPerson" placeholder="Enter name"></div>
  </div>
  <button class="btn" onclick="addTask()">Add Task</button>
 </div>
 <div class="panel">
  <h3>Task List</h3>
  <div class="table-wrap">
   <table id="taskTable">
    <thead><tr><th>Task</th><th>Due Date</th><th>Assigned To</th><th>Status</th><th>Action</th></tr></thead>
    <tbody></tbody>
   </table>
  </div>
 </div>
</section>

<!-- SEEDS -->
<section id="seeds" class="page">
 <h2 class="page-heading">🌱 Seed Inventory</h2>
 <div class="panel">
  <h3>Add Seed Stock</h3>
  <div class="form-grid">
   <div><label>Seed Name</label><input id="seedName" placeholder="Enter seed name"></div>
   <div><label>Quantity (kg)</label><input type="number" id="seedQty" placeholder="Enter quantity"></div>
   <div><label>Minimum Stock Alert (kg)</label><input type="number" id="seedMin" value="10"></div>
  </div>
  <button class="btn" onclick="addSeed()">Add Seed</button>
 </div>
 <div class="panel">
  <h3>Available Seeds</h3>
  <div class="table-wrap">
   <table id="seedTable">
    <thead><tr><th>Seed Name</th><th>Quantity</th><th>Stock Status</th><th>Action</th></tr></thead>
    <tbody></tbody>
   </table>
  </div>
 </div>
</section>

<!-- ECONOMICS -->
<section id="economics" class="page">
 <h2 class="page-heading">💰 Farm Economics</h2>
 <div class="panel">
  <h3>Farm Profit Calculator</h3>
  <div class="form-grid">
   <div><label>Expected Revenue (₹)</label><input type="number" id="revenue" placeholder="Enter revenue"></div>
   <div><label>Seed Cost (₹)</label><input type="number" id="seedCost" placeholder="Enter cost"></div>
   <div><label>Fertilizer Cost (₹)</label><input type="number" id="fertCost" placeholder="Enter cost"></div>
   <div><label>Labour Cost (₹)</label><input type="number" id="labourCost" placeholder="Enter cost"></div>
   <div><label>Other Expenses (₹)</label><input type="number" id="otherCost" placeholder="Enter cost"></div>
  </div>
  <button class="btn" onclick="calculateProfit()">Calculate Profit</button>
  <div class="result" id="profitResult">Your estimated profit will appear here.</div>
 </div>
 <div class="panel">
  <h3>Expense Tracker</h3>
  <div class="form-grid">
   <div><label>Expense Name</label><input id="expenseName" placeholder="Enter expense"></div>
   <div><label>Amount (₹)</label><input type="number" id="expenseAmount" placeholder="Enter amount"></div>
  </div>
  <button class="btn" onclick="addExpense()">Add Expense</button>
  <div class="table-wrap">
   <table id="expenseTable">
    <thead><tr><th>Expense</th><th>Amount</th><th>Action</th></tr></thead>
    <tbody></tbody>
   </table>
  </div>
  <h3 id="expenseTotal">Total Expenses: ₹0</h3>
 </div>
</section>

<!-- REPORTS -->
<section id="reports" class="page">
 <h2 class="page-heading">📊 Farm Reports</h2>
 <div class="panel">
  <h3>Farm Summary</h3>
  <div class="cards">
   <div class="card"><h3>Total Crops</h3><div class="number" id="reportCrops">4</div></div>
   <div class="card"><h3>Farm Area</h3><div class="number" id="reportArea">10</div><p>Acres</p></div>
   <div class="card"><h3>Water Usage</h3><div class="number">450 L</div></div>
  </div>
  <button class="btn" onclick="downloadReport()">Download Crop Report (CSV)</button>
  <button class="btn btn-blue" onclick="window.print()">Print Report</button>
 </div>
</section>

<!-- NOTIFICATIONS -->
<section id="notifications" class="page">
 <h2 class="page-heading">🔔 Notifications</h2>
 <div class="panel">
  <h3>Farm Notifications</h3>
  <button class="btn btn-red" onclick="clearNotifications()">Clear Notifications</button>
  <div id="notificationList">
   <div class="alert">Welcome to Smart Agriculture System.</div>
   <div class="alert">Please check your soil moisture regularly.</div>
  </div>
 </div>
</section>

<div class="footer">Smart Agriculture and Crop Management System | Academic Project Demo</div>
</main>
</div>

<script>
// PAGE NAVIGATION
function showPage(page,button){
 document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
 document.getElementById(page).classList.add("active");
 document.querySelectorAll(".nav-btn").forEach(b=>b.classList.remove("active"));
 if(button)button.classList.add("active");
 window.scrollTo({top:0,behavior:"smooth"});
}

// DATE
document.getElementById("todayDate").textContent =
 new Date().toLocaleDateString("en-IN",{weekday:"short",year:"numeric",month:"short",day:"numeric"});

// FARM DETAILS
function saveFarm(){
 let name=document.getElementById("farmName").value||"My Farm";
 let owner=document.getElementById("ownerName").value||"Not provided";
 let area=Number(document.getElementById("farmArea").value)||0;
 let location=document.getElementById("farmLocation").value||"Not provided";
 let soil=document.getElementById("farmSoil").value;
 let water=document.getElementById("waterSource").value;
 document.getElementById("farmAreaDisplay").textContent=area+" Acres";
 document.getElementById("reportArea").textContent=area;
 document.getElementById("farmInfo").textContent=
 "Farm: "+name+" | Owner: "+owner+" | Area: "+area+" Acres | Location: "+location+" | Soil: "+soil+" | Water: "+water;
 document.getElementById("farmResult").innerHTML='<div class="success">Farm details saved for this session.</div>';
 addNotification("Farm details updated.");
}

// CROP MANAGEMENT
function addCrop(){
 let name=document.getElementById("cropName").value.trim();
 let area=document.getElementById("cropArea").value;
 let sow=document.getElementById("sowingDate").value;
 let harvest=document.getElementById("harvestDate").value;
 if(!name||!area){alert("Please enter crop name and area.");return}
 let row=document.getElementById("cropTable").querySelector("tbody").insertRow();
 row.innerHTML=`<td>${escapeHTML(name)}</td><td>${Number(area)}</td><td>${escapeHTML(sow)}</td><td>${escapeHTML(harvest)}</td><td><span class="status">Growing</span></td><td><button class="btn btn-red" onclick="deleteCrop(this)">Delete</button></td>`;
 document.getElementById("cropName").value="";
 document.getElementById("cropArea").value="";
 updateCropCount();
 addNotification("New crop added: "+name);
}
function deleteCrop(btn){
 btn.closest("tr").remove();
 updateCropCount();
}
function updateCropCount(){
 let rows=document.querySelectorAll("#cropTable tbody tr");
 document.getElementById("cropCount").textContent=rows.length;
 document.getElementById("reportCrops").textContent=rows.length;
 updateCropChart();
}
function searchCrops(){
 let value=document.getElementById("cropSearch").value.toLowerCase();
 document.querySelectorAll("#cropTable tbody tr").forEach(row=>{
  row.style.display=row.cells[0].textContent.toLowerCase().includes(value)?"":"none";
 });
}

// CROP RECOMMENDATION
function recommendCrop(){
 let soil=document.getElementById("recSoil").value;
 let season=document.getElementById("recSeason").value;
 let water=document.getElementById("recWater").value;
 let suggestions=[];
 if(soil==="Black Soil")suggestions=["Cotton","Sorghum","Soybean"];
 else if(soil==="Red Soil")suggestions=["Groundnut","Millets","Pulses"];
 else if(soil==="Alluvial Soil")suggestions=["Paddy","Wheat","Sugarcane"];
 else suggestions=["Millets","Groundnut","Pulses"];
 if(water==="Low")suggestions=["Millets","Sorghum","Pulses"];
 if(season==="Rabi"&&water!=="Low")suggestions=["Wheat","Chickpea","Mustard"];
 if(season==="Summer")suggestions=["Groundnut","Green Gram","Vegetables"];
 document.getElementById("recommendResult").innerHTML=
 "<b>Suggested crops:</b> "+suggestions.join(", ")+
 "<br><b>Soil:</b> "+soil+"<br><b>Season:</b> "+season+
 "<br><b>Water availability:</b> "+water+
 "<br><small>These are general educational suggestions. Check local agricultural guidance and soil test results before planting.</small>";
}

// IRRIGATION
let pump=false;
function pumpOn(){
 pump=true;
 document.getElementById("pumpStatus").textContent="ON";
 document.getElementById("pumpMessage").textContent="Demo pump status: ON";
 addNotification("Demo irrigation pump switched ON.");
}
function pumpOff(){
 pump=false;
 document.getElementById("pumpStatus").textContent="OFF";
 document.getElementById("pumpMessage").textContent="Demo pump status: OFF";
 addNotification("Demo irrigation pump switched OFF.");
}
function autoIrrigation(){
 let moisture=Number(document.getElementById("moistureInput").value);
 if(moisture<40){
  pumpOn();
  document.getElementById("pumpMessage").textContent="Soil moisture is low. Demo automatic irrigation switched ON.";
 }else{
  pumpOff();
  document.getElementById("pumpMessage").textContent="Soil moisture is sufficient. Demo automatic irrigation remains OFF.";
 }
}

// SOIL MONITORING
function updateSoil(){
 let moisture=Number(document.getElementById("moistureInput").value);
 let ph=Number(document.getElementById("soilPH").value);
 let temp=Number(document.getElementById("soilTemp").value);
 let nitrogen=document.getElementById("nitrogen").value;
 if(moisture<0||moisture>100||ph<0||ph>14){alert("Enter valid soil values.");return}
 document.getElementById("moistureDisplay").textContent=moisture+"%";
 document.getElementById("irrigationMoisture").textContent=moisture+"%";
 let condition=moisture<30?"Low moisture":moisture<70?"Moderate moisture":"High moisture";
 document.getElementById("soilResult").innerHTML=
 "<b>Soil moisture:</b> "+moisture+"% ("+condition+")<br>"+
 "<b>Soil pH:</b> "+ph+"<br><b>Temperature:</b> "+temp+" °C<br>"+
 "<b>Nitrogen:</b> "+nitrogen;
 addNotification("Soil monitoring values updated.");
}

// FERTILIZER SCHEDULE
function addFertilizer(){
 let crop=document.getElementById("fertCrop").value.trim();
 let fert=document.getElementById("fertName").value.trim();
 let date=document.getElementById("fertDate").value;
 let qty=document.getElementById("fertQty").value.trim();
 if(!crop||!fert){alert("Enter crop and fertilizer name.");return}
 let row=document.querySelector("#fertTable tbody").insertRow();
 row.innerHTML=`<td>${escapeHTML(crop)}</td><td>${escapeHTML(fert)}</td><td>${escapeHTML(date)}</td><td>${escapeHTML(qty)}</td><td><button class="btn btn-red" onclick="this.closest('tr').remove()">Delete</button></td>`;
 addNotification("Fertilizer schedule added for "+crop+".");
}

// PEST MONITORING
function addPest(){
 let crop=document.getElementById("pestCrop").value.trim();
 let observation=document.getElementById("pestName").value.trim();
 let severity=document.getElementById("pestSeverity").value;
 let date=document.getElementById("pestDate").value;
 if(!crop||!observation){alert("Enter crop and observation.");return}
 let row=document.querySelector("#pestTable tbody").insertRow();
 row.innerHTML=`<td>${escapeHTML(crop)}</td><td>${escapeHTML(observation)}</td><td>${escapeHTML(severity)}</td><td>${escapeHTML(date)}</td><td><button class="btn btn-red" onclick="this.closest('tr').remove()">Delete</button></td>`;
 addNotification("Crop health observation added.");
}

// TASK PLANNER
function addTask(){
 let task=document.getElementById("taskName").value.trim();
 let date=document.getElementById("taskDate").value;
 let person=document.getElementById("taskPerson").value.trim();
 if(!task){alert("Enter task name.");return}
 let row=document.querySelector("#taskTable tbody").insertRow();
 row.innerHTML=`<td>${escapeHTML(task)}</td><td>${escapeHTML(date)}</td><td>${escapeHTML(person)}</td><td><span class="status">Pending</span></td><td><button class="btn" onclick="completeTask(this)">Complete</button><button class="btn btn-red" onclick="this.closest('tr').remove()">Delete</button></td>`;
 addNotification("New farm task added: "+task);
}
function completeTask(btn){
 btn.closest("tr").cells[3].innerHTML='<span class="status">Completed</span>';
 btn.remove();
}

// SEED INVENTORY
function addSeed(){
 let name=document.getElementById("seedName").value.trim();
 let qty=Number(document.getElementById("seedQty").value);
 let min=Number(document.getElementById("seedMin").value);
 if(!name||!Number.isFinite(qty)||qty<0){alert("Enter valid seed details.");return}
 let status=qty<=min?"Low Stock":"Available";
 let row=document.querySelector("#seedTable tbody").insertRow();
 row.innerHTML=`<td>${escapeHTML(name)}</td><td>${qty} kg</td><td>${status}</td><td><button class="btn btn-red" onclick="this.closest('tr').remove()">Delete</button></td>`;
 if(qty<=min)addNotification("Low seed stock: "+name);
 else addNotification("Seed stock added: "+name);
}

// FARM ECONOMICS
function calculateProfit(){
 let revenue=Number(document.getElementById("revenue").value)||0;
 let seed=Number(document.getElementById("seedCost").value)||0;
 let fert=Number(document.getElementById("fertCost").value)||0;
 let labour=Number(document.getElementById("labourCost").value)||0;
 let other=Number(document.getElementById("otherCost").value)||0;
 let expenses=seed+fert+labour+other;
 let profit=revenue-expenses;
 document.getElementById("incomeDisplay").textContent="₹"+revenue.toLocaleString("en-IN");
 document.getElementById("profitResult").innerHTML=
 "<b>Total Revenue:</b> ₹"+revenue.toLocaleString("en-IN")+
 "<br><b>Total Expenses:</b> ₹"+expenses.toLocaleString("en-IN")+
 "<br><b>Estimated Profit:</b> ₹"+profit.toLocaleString("en-IN");
}
function addExpense(){
 let name=document.getElementById("expenseName").value.trim();
 let amount=Number(document.getElementById("expenseAmount").value);
 if(!name||!Number.isFinite(amount)||amount<0){alert("Enter valid expense details.");return}
 let row=document.querySelector("#expenseTable tbody").insertRow();
 row.innerHTML=`<td>${escapeHTML(name)}</td><td>${amount.toLocaleString("en-IN")}</td><td><button class="btn btn-red" onclick="this.closest('tr').remove();updateExpenseTotal()">Delete</button></td>`;
 updateExpenseTotal();
}
function updateExpenseTotal(){
 let total=0;
 document.querySelectorAll("#expenseTable tbody tr").forEach(row=>{
  total+=Number(row.cells[1].textContent.replace(/,/g,""))||0;
 });
 document.getElementById("expenseTotal").textContent="Total Expenses: ₹"+total.toLocaleString("en-IN");
}

// NOTIFICATIONS
function addNotification(message){
 let list=document.getElementById("notificationList");
 let item=document.createElement("div");
 item.className="alert";
 item.textContent=message+" — "+new Date().toLocaleTimeString();
 list.prepend(item);
 document.getElementById("alertCount").textContent=list.children.length;
}
function clearNotifications(){
 document.getElementById("notificationList").innerHTML="";
 document.getElementById("alertCount").textContent="0";
}

// CSV REPORT
function downloadReport(){
 let rows=[["Crop Name","Area","Sowing Date","Harvest Date","Status"]];
 document.querySelectorAll("#cropTable tbody tr").forEach(row=>{
  if(row.style.display!=="none"){
   rows.push([...row.cells].slice(0,5).map(c=>c.textContent.trim()));
  }
 });
 let csv=rows.map(row=>row.map(value=>'"'+String(value).replace(/"/g,'""')+'"').join(",")).join("\n");
 let blob=new Blob([csv],{type:"text/csv;charset=utf-8;"});
 let url=URL.createObjectURL(blob);
 let a=document.createElement("a");
 a.href=url;
 a.download="smart-agriculture-crop-report.csv";
 a.click();
 URL.revokeObjectURL(url);
}

// SAFE TEXT
function escapeHTML(value){
 return String(value).replace(/[&<>"']/g,function(char){
  return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[char];
 });
}

// CHARTS
let waterChart,cropChart;

function updateCropChart(){
 if(!cropChart)return;
 let names={},areas={};
 document.querySelectorAll("#cropTable tbody tr").forEach(row=>{
  let name=row.cells[0].textContent;
  let area=Number(row.cells[1].textContent)||0;
  names[name]=(names[name]||0)+area;
 });
 cropChart.data.labels=Object.keys(names);
 cropChart.data.datasets[0].data=Object.values(names);
 cropChart.update();
}

window.addEventListener("load",function(){
 if(typeof Chart==="undefined"){
  document.querySelectorAll(".chart-box,.small-chart").forEach(el=>{
   el.innerHTML="Charts require an internet connection to load Chart.js.";
  });
  return;
 }

 waterChart=new Chart(document.getElementById("waterChart"),{
  type:"line",
  data:{
   labels:["Mon","Tue","Wed","Thu","Fri","Sat","Sun"],
   datasets:[{
    label:"Water Usage (Litres)",
    data:[300,450,380,520,410,600,450],
    borderColor:"#9cff83",
    backgroundColor:"rgba(156,255,131,.16)",
    fill:true,
    tension:.4
   }]
  },
  options:{
   responsive:true,
   maintainAspectRatio:false,
   plugins:{legend:{labels:{color:"white"}}},
   scales:{
    x:{ticks:{color:"white"},grid:{color:"rgba(255,255,255,.12)"}},
    y:{ticks:{color:"white"},grid:{color:"rgba(255,255,255,.12)"}}
   }
  }
 });

 cropChart=new Chart(document.getElementById("cropChart"),{
  type:"doughnut",
  data:{
   labels:["Paddy","Wheat","Cotton","Maize"],
   datasets:[{data:[3,2,3,2],backgroundColor:["#75c95d","#e3bb55","#d18b54","#82c6b0"],borderWidth:1}]
  },
  options:{
   responsive:true,
   maintainAspectRatio:false,
   plugins:{legend:{position:"bottom",labels:{color:"white",boxWidth:12}}}
  }
 });
 updateCropChart();
});
</script>
</body>
</html>

