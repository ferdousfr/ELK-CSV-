
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OpsHub - DLR Report Generator</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<style>
:root {
    --primary:#e3b400;
    --primary-dark:#b58b00;
    --dark:#202b45;
    --muted:#718096;
    --border:#e1e7f0;
    --background:#f7f8fc;
    --success:#16834a;
    --danger:#d04444;
    --warning:#c58a00;
    --yellow-light:#fff8d9;
}
*{box-sizing:border-box}
body{margin:0;background:var(--background);color:var(--dark);font-family:Arial,sans-serif;font-size:14px}
button,input,select{font:inherit}
.app{display:flex;min-height:100vh}
.sidebar{width:220px;background:#fff;border-right:1px solid var(--border);padding:24px 14px;flex-shrink:0}
.brand{color:#202b45;font-size:19px;font-weight:800;line-height:1.4;margin:0 10px 35px;border-left:5px solid var(--primary);padding-left:10px}
.nav{padding:13px 12px;border-radius:8px;margin-bottom:5px;color:#586780}
.nav.active{background:var(--yellow-light);color:#8c6a00;font-weight:bold;border-left:3px solid var(--primary)}
.main{flex:1;min-width:0}
.topbar{background:white;border-bottom:1px solid var(--border);padding:14px 25px;display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap}
.clock-wrap{background:#202b45;color:white;border:2px solid var(--primary);border-radius:12px;padding:9px 15px;min-width:235px;text-align:center;box-shadow:0 3px 10px rgba(0,0,0,.10)}
.clock-label{display:block;color:#ffdf63;font-size:10px;font-weight:bold;letter-spacing:1.5px;margin-bottom:5px}
.clock-main{font-size:20px;font-weight:bold;letter-spacing:1px}
.clock-sub{display:block;color:#dce2ed;font-size:11px;margin-top:4px}
.tabs{background:white;border-bottom:1px solid var(--border);display:flex;gap:25px;padding:15px 25px;overflow-x:auto}
.tabs span{white-space:nowrap;color:#65728a}
.tabs .active{color:#927000;font-weight:bold;border-bottom:3px solid var(--primary);padding-bottom:10px}
.content{max-width:1350px;margin:auto;padding:25px}
.page-title{font-size:25px;margin:0 0 22px}
.card{background:white;border:1px solid var(--border);border-radius:12px;margin-bottom:20px;overflow:hidden;box-shadow:0 3px 12px rgba(30,50,90,.035)}
.card-title{padding:17px 22px;border-bottom:1px solid #edf0f5;border-left:4px solid var(--primary);font-weight:bold;font-size:15px;display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap}
.card-body{padding:22px}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:18px}
.field label{display:block;margin-bottom:8px;color:var(--muted);font-size:12px;font-weight:bold}
.field input,.field select{width:100%;padding:12px;border:1px solid #ccd5e4;border-radius:7px;background:white;color:var(--dark)}
.field input:focus,.field select:focus{outline:none;border-color:var(--primary-dark);box-shadow:0 0 0 3px rgba(227,180,0,.14)}
.upload-grid{display:grid;grid-template-columns:1fr 1fr;gap:18px}
.upload-box{text-align:center;padding:25px 18px;border:1px dashed #bdc9dd;border-radius:10px;background:#fffdf4}
.upload-box h3{margin:0 0 10px}
.upload-box input{width:100%;margin-top:12px}
.file-status{color:var(--muted);font-size:12px;margin-top:12px;overflow-wrap:anywhere}
.btn{padding:11px 16px;border:none;border-radius:7px;background:var(--primary);color:#202b45;font-weight:bold;cursor:pointer;transition:.2s}
.btn:hover{background:#f0c72c;transform:translateY(-1px)}
.btn.secondary{background:#edf0f7;color:#34425e}
.btn.secondary:hover{background:#fff0b8}
.btn.small{padding:8px 12px;font-size:11px}
.actions{display:flex;flex-wrap:wrap;gap:9px;margin-top:15px}
.status-message{color:var(--muted);margin:15px 0 0;line-height:1.5}
.small-note{color:var(--muted);font-size:12px;line-height:1.6}
.report{background:white;color:#1c2433;padding:32px;border:1px solid #e0e5ed}
.report-header{display:flex;justify-content:space-between;align-items:center;gap:15px;margin-bottom:25px}
.report-logo{max-width:180px;max-height:55px;object-fit:contain}
.report-company{color:#63718a;font-size:12px;letter-spacing:1.5px;font-weight:bold}
.report h2{font-family:Georgia,serif;font-size:34px;font-weight:normal;margin:0 0 10px}
.period{color:#77839a;font-size:14px;margin-bottom:25px;overflow-wrap:anywhere}
.summary{display:flex;flex-wrap:wrap;gap:28px;margin:22px 0;font-family:monospace;font-size:16px}
.summary strong{color:#1d2d4b}
.report table{width:100%;border-collapse:collapse;font-family:monospace}
.report th,.report td{padding:12px;border:1px solid #d8deea;text-align:left}
.report th{background:#fff2b8;font-weight:bold}
.report td:nth-child(3),.report th:nth-child(3),.report td:nth-child(4),.report th:nth-child(4){text-align:right}
.report td:nth-child(4){color:#927000;font-weight:bold}
.report-meta{margin-top:28px;padding-top:15px;border-top:2px solid #e7c54e;font-family:monospace;font-weight:bold;line-height:2;overflow-wrap:anywhere}
.report-status{color:var(--success)}
.empty-row{text-align:center!important;color:#8993a5}
.company-edit{display:flex;gap:9px;align-items:end;flex-wrap:wrap}
.company-edit .field{flex:1;min-width:200px}
.reporter-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:10px}
.reporter-item{display:flex;align-items:center;gap:8px;padding:9px;border:1px solid var(--border);border-radius:8px;background:#fff}
.reporter-item.selected{background:var(--yellow-light);border-color:var(--primary-dark)}
.reporter-item input[type=checkbox]{width:17px;height:17px;accent-color:#c49a00;flex-shrink:0;cursor:pointer}
.reporter-item input[type=text]{width:100%;min-width:0;padding:9px;border:1px solid #d6dce6;border-radius:6px;font-size:12px}
.dashboard-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px}
.stat-card{padding:16px;border:1px solid var(--border);border-top:4px solid var(--primary);border-radius:9px;background:#fff}
.stat-card small{display:block;color:var(--muted);font-size:11px;font-weight:bold}
.stat-card strong{display:block;margin-top:8px;font-size:25px}
.stat-card.success{border-top-color:var(--success)}
.stat-card.error{border-top-color:var(--danger)}
.stat-card.warning{border-top-color:var(--warning)}
.dashboard-status{display:grid;grid-template-columns:180px 1fr;gap:15px;margin-top:15px;padding:15px;border:1px solid var(--border);border-radius:9px;background:#fffdf4}
.status-pill{display:inline-block;padding:7px 14px;border-radius:20px;background:#e4f5eb;color:var(--success);font-size:12px;font-weight:bold}
.status-pill.warning{background:#fff1d5;color:#a66c00}
.status-pill.critical{background:#ffe6e6;color:var(--danger)}
.status-detail{font-size:12px;line-height:1.8}
.status-edit{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:10px}
.status-edit input,.status-edit select{width:100%;padding:9px;border:1px solid #ccd5e4;border-radius:7px}
.status-edit label{display:block;font-size:11px;color:var(--muted);font-weight:bold;margin-bottom:6px}
@media(max-width:950px){.reporter-grid{grid-template-columns:repeat(2,minmax(0,1fr))}.dashboard-grid{grid-template-columns:repeat(2,minmax(0,1fr))}}
@media(max-width:850px){.sidebar{display:none}.content{padding:14px}.grid,.upload-grid{grid-template-columns:1fr}.report{padding:18px}.report h2{font-size:25px}.report th,.report td{padding:8px 5px;font-size:11px}.summary{gap:13px;font-size:13px}.clock-wrap{min-width:200px}}
@media(max-width:560px){.reporter-grid{grid-template-columns:1fr}.dashboard-status{grid-template-columns:1fr}.status-edit{grid-template-columns:1fr}}
</style>
</head>

<body>
<div class="app">

<aside class="sidebar">
    <div class="brand">INFOZILLION<br>TELETECH BD</div>
    <div class="nav">Dashboard</div>
    <div class="nav">Daily Shift Report</div>
    <div class="nav">9xxx Report</div>
    <div class="nav">1xxx Report</div>
    <div class="nav">4xx/5xx Report</div>
    <div class="nav active">DLR Report</div>
    <div class="nav">Delay Report</div>
    <div class="nav">MNP Status Report</div>
</aside>

<div class="main">
<header class="topbar">
    <div>Dashboard / <strong>DLR Report</strong></div>
    <div class="clock-wrap">
        <span class="clock-label">BANGLADESH TIME · UTC+6</span>
        <div class="clock-main" id="clock12">--:--:-- --</div>
        <span class="clock-sub" id="clock24">--:--:--</span>
        <span class="clock-sub" id="clockDate"></span>
    </div>
</header>

<div class="tabs">
    <span>9xxx Report</span><span>1xxx Report</span>
    <span>4xx/5xx Report</span><span class="active">DLR Report</span>
    <span>Delay Report</span>
</div>

<main class="content">
<h1 class="page-title">DLR <span style="color:#c49a00">Report Generator</span></h1>

<!-- COMPANY NAME -->
<section class="card">
    <div class="card-title">
        <span>Company Information</span>
        <button class="btn small" onclick="saveSettings()">Save Changes</button>
    </div>
    <div class="card-body">
        <div class="company-edit">
            <div class="field">
                <label>Company Name</label>
                <input id="companyName" type="text" value="INFOZILLION TELETECH BD" placeholder="Enter company name">
            </div>
            <button class="btn" onclick="saveSettings()">Save Company Name</button>
        </div>
        <p class="small-note">Company name will appear in both MNO and IPTSP reports.</p>
    </div>
</section>

<!-- REPORTER NAMES -->
<section class="card">
    <div class="card-title">
        <span>Report Prepared By – 11 Persons</span>
        <button class="btn small" onclick="saveSettings()">Save Names</button>
    </div>
    <div class="card-body">
        <div class="reporter-grid" id="reporterGrid"></div>
        <p class="small-note">Enter the 11 names when needed. Select only the person who prepared the report. Only one person can be selected at a time. Names are saved automatically.</p>
    </div>
</section>

<!-- DASHBOARD -->
<section class="card">
    <div class="card-title">
        <span>Dashboard Statistics</span>
        <button class="btn small secondary" onclick="refreshDashboard()">Refresh</button>
    </div>
    <div class="card-body">
        <div class="dashboard-grid">
            <div class="stat-card">
                <small>TOTAL MESSAGES</small>
                <strong id="dashTotal">0</strong>
            </div>
            <div class="stat-card success">
                <small>SUCCESS COUNT</small>
                <strong id="dashSuccess">0</strong>
            </div>
            <div class="stat-card error">
                <small>ERROR COUNT</small>
                <strong id="dashErrors">0</strong>
            </div>
            <div class="stat-card warning">
                <small>ERROR PERCENTAGE</small>
                <strong id="dashErrorPct">0.00%</strong>
            </div>
        </div>

        <div class="dashboard-status">
            <div>
                <label style="display:block;font-size:11px;font-weight:bold;color:#718096;margin-bottom:9px">CURRENT STATUS</label>
                <span id="dashboardStatus" class="status-pill">NORMAL</span>
            </div>
            <div>
                <div class="status-edit">
                    <div>
                        <label>Report Status (Editable)</label>
                        <input id="reportStatus" value="Normal" placeholder="Normal">
                    </div>
                    <div>
                        <label>Automatic Error Threshold (%)</label>
                        <input id="errorThreshold" type="number" min="0" max="100" step="0.01" value="5">
                    </div>
                </div>
                <div id="dashboardErrorDetails" class="status-detail">
                    Upload CSV files to see error statistics.
                </div>
                <p class="small-note">Automatic alert: Warning at the selected threshold and Critical at twice the threshold. Manual report status remains editable.</p>
            </div>
        </div>
    </div>
</section>

<!-- MONITORING WINDOW -->
<section class="card">
    <div class="card-title">Monitoring Window</div>
    <div class="card-body">
        <strong id="monitoringInfo">Not generated yet</strong>
        <p class="small-note">Monitoring window is automatically calculated from the earliest and latest values in the CSV @timestamp column.</p>
    </div>
</section>

<!-- REPORT INFORMATION -->
<section class="card">
    <div class="card-title">Report Information</div>
    <div class="card-body grid">
        <div class="field">
            <label>Selected Reporter</label>
            <input id="selectedReporterDisplay" readonly placeholder="Select a person above">
        </div>
        <div class="field">
            <label>Company Logo (Optional)</label>
            <input type="file" id="logo" accept="image/*">
        </div>
    </div>
</section>

<!-- UPLOAD -->
<section class="card">
    <div class="card-title">Upload DLR CSV Files</div>
    <div class="card-body upload-grid">
        <div class="upload-box">
            <h3>📁 DLR MNO</h3>
            <p class="small-note">Upload MNO CSV file</p>
            <input type="file" id="mnoFile" accept=".csv">
            <div class="file-status" id="mnoFileStatus">No file selected</div>
        </div>
        <div class="upload-box">
            <h3>📁 DLR IPTSP</h3>
            <p class="small-note">Upload IPTSP CSV file</p>
            <input type="file" id="iptspFile" accept=".csv">
            <div class="file-status" id="iptspFileStatus">No file selected</div>
        </div>
    </div>
</section>

<!-- GENERATE / EXPORT -->
<section class="card">
    <div class="card-title">Generate and Export Reports</div>
    <div class="card-body">
        <div class="actions">
            <button class="btn" onclick="generateReport('mno')">Generate MNO Report</button>
            <button class="btn" onclick="generateReport('iptsp')">Generate IPTSP Report</button>
        </div>
        <div class="actions">
            <button class="btn secondary" onclick="downloadImage('mno','png')">MNO PNG</button>
            <button class="btn secondary" onclick="downloadImage('mno','jpg')">MNO JPG</button>
            <button class="btn secondary" onclick="downloadPDF('mno')">MNO PDF</button>
            <button class="btn secondary" onclick="downloadCSV('mno')">MNO Summary CSV</button>
            <button class="btn secondary" onclick="copyImage('mno')">Copy MNO Image</button>
        </div>
        <div class="actions">
            <button class="btn secondary" onclick="downloadImage('iptsp','png')">IPTSP PNG</button>
            <button class="btn secondary" onclick="downloadImage('iptsp','jpg')">IPTSP JPG</button>
            <button class="btn secondary" onclick="downloadPDF('iptsp')">IPTSP PDF</button>
            <button class="btn secondary" onclick="downloadCSV('iptsp')">IPTSP Summary CSV</button>
            <button class="btn secondary" onclick="copyImage('iptsp')">Copy IPTSP Image</button>
        </div>
        <p id="message" class="status-message">Upload a CSV file to generate a report.</p>
    </div>
</section>

<!-- MNO PREVIEW -->
<section class="card">
    <div class="card-title">DLR MNO Report Preview</div>
    <div class="card-body">
        <div class="report" id="mnoReport">
            <div class="report-header">
                <div class="report-company">
                    <span class="company-report-name">INFOZILLION TELETECH BD</span><br>
                    SERVICE ASSURANCE
                </div>
                <img class="report-logo" id="mnoLogo" alt="" style="display:none">
            </div>
            <h2>DLR Report — MNO</h2>
            <div class="period" id="mnoPeriod">Monitoring Window: Not available</div>
            <div class="summary">
                <span>Total: <strong id="mnoTotal">0</strong></span>
                <span>Success: <strong id="mnoSuccess">0</strong></span>
                <span>Error: <strong id="mnoErrors">0</strong></span>
            </div>
            <table>
                <thead><tr><th>Status Code</th><th>Error Description</th><th>Count</th><th>Percentage</th></tr></thead>
                <tbody id="mnoRows"><tr><td colspan="4" class="empty-row">No data loaded</td></tr></tbody>
            </table>
            <div class="report-meta">
                Reporter: <span class="reporter-name">Not specified</span><br>
                Status: <span class="report-status">Normal</span>
            </div>
        </div>
    </div>
</section>

<!-- IPTSP PREVIEW -->
<section class="card">
    <div class="card-title">DLR IPTSP Report Preview</div>
    <div class="card-body">
        <div class="report" id="iptspReport">
            <div class="report-header">
                <div class="report-company">
                    <span class="company-report-name">INFOZILLION TELETECH BD</span><br>
                    SERVICE ASSURANCE
                </div>
                <img class="report-logo" id="iptspLogo" alt="" style="display:none">
            </div>
            <h2>DLR Report — IPTSP</h2>
            <div class="period" id="iptspPeriod">Monitoring Window: Not available</div>
            <div class="summary">
                <span>Total: <strong id="iptspTotal">0</strong></span>
                <span>Success: <strong id="iptspSuccess">0</strong></span>
                <span>Error: <strong id="iptspErrors">0</strong></span>
            </div>
            <table>
                <thead><tr><th>Status Code</th><th>Error Description</th><th>Count</th><th>Percentage</th></tr></thead>
                <tbody id="iptspRows"><tr><td colspan="4" class="empty-row">No data loaded</td></tr></tbody>
            </table>
            <div class="report-meta">
                Reporter: <span class="reporter-name">Not specified</span><br>
                Status: <span class="report-status">Normal</span>
            </div>
        </div>
    </div>
</section>

</main>
</div>
</div>

<script>
/* OFFICIAL ERROR CODE MAPPING */
const DLR_ERROR_DESCRIPTIONS = {
    "1000":"Success",
    "1001":"IP Blacklist",
    "1002":"Invalid Username",
    "1003":"Invalid Password",
    "1004":"Parameter missing",
    "1005":"Invalid Parameter",
    "1006":"CLI/Masking Invalid",
    "1007":"Account Barred",
    "1008":"Insufficient Balance",
    "1009":"DND User",
    "1010":"Invalid MSISDN",
    "1011":"Duplicate Transaction ID",
    "1012":"Message lengths exceed",
    "1013":"No Request found",
    "1014":"Delivery pending",
    "1015":"TPS Limit Exceeded",
    "1016":"Number Barred",
    "1017":"API is not allowed for user",
    "1018":"No Live Campaign",
    "1019":"Messagebody Invalid",
    "1020":"Internal Server Error",
    "1021":"CLI/Masking Already Exists",
    "1050":"Allowed campaigns limit exceeded",
    "1051":"Allowed SMS quota is completed",
    "1052":"Submission record not found",
    "1053":"Invalid Transaction Id",
    "1054":"MSISDN Limit Exceeded",
    "1429":"Too Many Request. Try in a Minute."
};

const $ = id => document.getElementById(id);
const reportData = {mno:null,iptsp:null};
let logoData = "";

/* CLOCK */
function updateClock(){
    const now=new Date();
    const options={timeZone:"Asia/Dhaka",hour:"2-digit",minute:"2-digit",second:"2-digit"};
    $("clock12").textContent=new Intl.DateTimeFormat("en-US",{...options,hour12:true}).format(now);
    $("clock24").textContent="24-hour: "+new Intl.DateTimeFormat("en-GB",{...options,hour12:false}).format(now);
    $("clockDate").textContent=new Intl.DateTimeFormat("en-GB",{timeZone:"Asia/Dhaka",weekday:"short",day:"2-digit",month:"short",year:"numeric"}).format(now);
}
updateClock();
setInterval(updateClock,1000);

/* SAFE HTML */
function escapeHTML(value){
    return String(value??"").replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
}

/* SETTINGS SAVE / LOAD */
function getSettings(){
    try{return JSON.parse(localStorage.getItem("opshubDLRSettings")||"{}");}
    catch(e){return {};}
}
function saveSettings(){
    const names=[...document.querySelectorAll(".reporter-name-input")].map(x=>x.value);
    const selected=document.querySelector('input[name="reporterSelect"]:checked');
    const settings={
        companyName:$("companyName").value,
        reportStatus:$("reportStatus").value,
        errorThreshold:$("errorThreshold").value,
        reporterNames:names,
        selectedReporter:selected?Number(selected.value):-1
    };
    localStorage.setItem("opshubDLRSettings",JSON.stringify(settings));
    updateReportInformation();
    $("message").textContent="Settings saved successfully.";
}
function loadSettings(){
    const s=getSettings();
    $("companyName").value=s.companyName||"INFOZILLION TELETECH BD";
    $("reportStatus").value=s.reportStatus||"Normal";
    $("errorThreshold").value=s.errorThreshold??5;
    renderReporterNames(s.reporterNames||Array(11).fill(""),s.selectedReporter??-1);
    updateReportInformation();
}
function renderReporterNames(names,selectedIndex){
    $("reporterGrid").innerHTML="";
    for(let i=0;i<11;i++){
        const item=document.createElement("div");
        item.className="reporter-item";
        item.innerHTML=`
            <input type="checkbox" name="reporterSelect" value="${i}" aria-label="Select reporter">
            <input type="text" class="reporter-name-input" placeholder="Person ${i+1}" aria-label="Person ${i+1} name">
        `;
        const checkbox=item.querySelector('input[type="checkbox"]');
        const text=item.querySelector('input[type="text"]');
        text.value=names[i]||"";
        checkbox.checked=selectedIndex===i;
        checkbox.addEventListener("change",()=>{
            if(checkbox.checked){
                document.querySelectorAll('input[name="reporterSelect"]').forEach(x=>{
                    if(x!==checkbox)x.checked=false;
                });
            }
            updateReporterHighlight();
            saveSettings();
        });
        text.addEventListener("input",saveSettings);
        $("reporterGrid").appendChild(item);
    }
    updateReporterHighlight();
}
function updateReporterHighlight(){
    document.querySelectorAll(".reporter-item").forEach(item=>{
        item.classList.toggle("selected",item.querySelector('input[type="checkbox"]').checked);
    });
}
function getSelectedReporter(){
    const selected=document.querySelector('input[name="reporterSelect"]:checked');
    if(!selected)return "Not specified";
    const name=selected.closest(".reporter-item").querySelector("input[type=text]").value.trim();
    return name||"Name not entered";
}

/* REPORT INFORMATION */
function updateReportInformation(){
    const company=$("companyName").value.trim()||"Company Name";
    const reporter=getSelectedReporter();
    const status=$("reportStatus").value.trim()||"Normal";

    document.querySelectorAll(".company-report-name").forEach(x=>x.textContent=company);
    document.querySelectorAll(".reporter-name").forEach(x=>x.textContent=reporter);
    document.querySelectorAll(".report-status").forEach(x=>{
        x.textContent=status;
        x.style.color=/resolved|normal|completed|stable/i.test(status)?"#16834a":/fail|error|critical|persist/i.test(status)?"#d04444":"#a07800";
    });
    $("selectedReporterDisplay").value=reporter;
}
$("companyName").addEventListener("input",()=>{updateReportInformation();saveSettings();});
$("reportStatus").addEventListener("input",()=>{updateReportInformation();saveSettings();});
$("errorThreshold").addEventListener("input",()=>{saveSettings();refreshDashboard();});

/* CSV PARSER */
function parseCSV(text){
    text=text.replace(/^\uFEFF/,"");
    const firstLine=text.split(/\r?\n/)[0]||"";
    const delimiters=[",",";","\t","|"];
    const delimiter=delimiters.reduce((best,current)=>firstLine.split(current).length>firstLine.split(best).length?current:best,",");
    const rows=[];let row=[];let cell="";let quoted=false;
    for(let i=0;i<text.length;i++){
        const char=text[i];
        if(char==='"'&&quoted&&text[i+1]==='"'){cell+='"';i++;}
        else if(char==='"'){quoted=!quoted;}
        else if(char===delimiter&&!quoted){row.push(cell);cell="";}
        else if((char==="\n"||char==="\r")&&!quoted){
            if(char==="\r"&&text[i+1]==="\n")i++;
            row.push(cell);
            if(row.some(v=>v.trim()!==""))rows.push(row);
            row=[];cell="";
        }else{cell+=char;}
    }
    row.push(cell);
    if(row.some(v=>v.trim()!==""))rows.push(row);
    return rows;
}

/* COLUMN FINDER */
function findColumn(headers,possibleNames){
    return headers.findIndex(header=>possibleNames.includes(header.toLowerCase().trim()));
}

/* STATUS CODE EXTRACTION */
function extractStatusCode(row,headers,messageIndex){
    const statusIndex=findColumn(headers,[
        "statuscode","status_code","status code","errorcode","error_code",
        "error code","responsecode","response_code","response code",
        "ansresponsecode","ans_response_code","ans response code"
    ]);
    if(statusIndex>=0){
        const value=(row[statusIndex]||"").trim();
        if(/^\d{3,5}$/.test(value))return value;
    }
    const message=messageIndex>=0?(row[messageIndex]||"").trim():"";
    if(!message)return "Unknown";
    const patterns=[
        /"(?:statusCode|status_code|errorCode|error_code|responseCode|response_code|ansResponseCode|code|status)"\s*:\s*["']?(\d{3,5})/i,
        /(?:statusCode|status_code|errorCode|error_code|responseCode|response_code|ansResponseCode|code|status)\s*[=:]\s*["']?(\d{3,5})/i,
        /^\s*(\d{3,5})(?:\s*[:\-]|$)/,
        /(?:HTTP|http)\s+(\d{3,5})\b/
    ];
    for(const pattern of patterns){const match=message.match(pattern);if(match)return match[1];}
    return "Unknown";
}

/* TIMESTAMP PARSER */
function parseTimestamp(value){
    if(!value)return null;
    value=value.trim();
    const match=value.match(/^([A-Za-z]{3})\s+(\d{1,2}),\s*(\d{4})\s*@\s*(\d{1,2}):(\d{2}):(\d{2})(?:\.(\d{1,3}))?$/);
    if(match){
        const months={Jan:0,Feb:1,Mar:2,Apr:3,May:4,Jun:5,Jul:6,Aug:7,Sep:8,Oct:9,Nov:10,Dec:11};
        return new Date(Number(match[3]),months[match[1]],Number(match[2]),Number(match[4]),Number(match[5]),Number(match[6]),Number((match[7]||"0").padEnd(3,"0")));
    }
    const parsed=new Date(value);
    return isNaN(parsed.getTime())?null:parsed;
}
function formatTimestamp(date){
    const month=date.toLocaleString("en-US",{month:"short"});
    const day=String(date.getDate()).padStart(2,"0");
    const year=date.getFullYear();
    const hours=String(date.getHours()).padStart(2,"0");
    const minutes=String(date.getMinutes()).padStart(2,"0");
    const seconds=String(date.getSeconds()).padStart(2,"0");
    const milliseconds=String(date.getMilliseconds()).padStart(3,"0");
    return `${month} ${day}, ${year} @ ${hours}:${minutes}:${seconds}.${milliseconds}`;
}

/* ANALYZE CSV */
function analyzeCSV(text){
    const rows=parseCSV(text);
    if(rows.length<2)throw new Error("CSV file has no data rows.");
    const headers=rows[0].map(h=>h.trim().toLowerCase());
    const messageIndex=findColumn(headers,["message","response","responsemessage","response_message","ansresponsemessage","ans_response_message"]);
    const timestampIndex=findColumn(headers,["@timestamp","timestamp"]);
    if(timestampIndex<0)throw new Error('The CSV file must contain an "@timestamp" column.');

    const counts={};const timestamps=[];
    for(let i=1;i<rows.length;i++){
        const row=rows[i];
        if(!row||row.every(v=>!v.trim()))continue;
        const code=extractStatusCode(row,headers,messageIndex);
        if(!counts[code])counts[code]={code,description:DLR_ERROR_DESCRIPTIONS[code]||"Unknown Error Code",count:0};
        counts[code].count++;
        const timestamp=parseTimestamp(row[timestampIndex]);
        if(timestamp)timestamps.push(timestamp);
    }
    if(!Object.keys(counts).length)throw new Error("No valid records found in CSV.");
    if(!timestamps.length)throw new Error('No valid timestamps found in "@timestamp".');
    timestamps.sort((a,b)=>a-b);

    const list=Object.values(counts);
    const total=list.reduce((sum,item)=>sum+item.count,0);
    const success=counts["1000"]?counts["1000"].count:0;
    return {counts:list,total,success,errors:total-success,start:timestamps[0],end:timestamps[timestamps.length-1]};
}

/* FILE SELECTION */
["mno","iptsp"].forEach(type=>{
    $(type+"File").addEventListener("change",function(){
        $(""+type+"FileStatus").textContent=this.files[0]?this.files[0].name:"No file selected";
    });
});

/* GENERATE REPORT */
async function generateReport(type){
    const fileInput=$(type+"File");
    try{
        if(!fileInput.files.length)throw new Error("Please select the "+type.toUpperCase()+" CSV file first.");
        $("message").textContent="Processing CSV file...";
        const text=await fileInput.files[0].text();
        const result=analyzeCSV(text);
        reportData[type]=result;
        renderReport(type,result);
        refreshDashboard();
        $("message").textContent=type.toUpperCase()+" report generated successfully.";
    }catch(error){$("message").textContent="Error: "+error.message;}
}

/* RENDER REPORT */
function renderReport(type,data){
    const tbody=$(type+"Rows");
    tbody.innerHTML="";
    const sorted=[...data.counts].sort((a,b)=>{
        if(a.code==="1000")return -1;
        if(b.code==="1000")return 1;
        return a.code.localeCompare(b.code,undefined,{numeric:true});
    });
    sorted.forEach(item=>{
        const tr=document.createElement("tr");
        const pct=data.total?(item.count/data.total*100).toFixed(2):"0.00";
        [item.code,item.description,item.count.toLocaleString(),pct+"%"].forEach((value,index)=>{
            const td=document.createElement("td");
            td.textContent=value;
            if(index===3){td.style.color="#927000";td.style.fontWeight="bold";}
            tr.appendChild(td);
        });
        tbody.appendChild(tr);
    });
    $(type+"Total").textContent=data.total.toLocaleString();
    $(type+"Success").textContent=data.success.toLocaleString();
    $(type+"Errors").textContent=data.errors.toLocaleString();
    $(type+"Period").textContent=formatTimestamp(data.start)+" - "+formatTimestamp(data.end);
    $("monitoringInfo").textContent=formatTimestamp(data.start)+" - "+formatTimestamp(data.end);
    updateReportInformation();
}

/* DASHBOARD – COMBINES MNO + IPTSP DATA */
function refreshDashboard(){
    const sources=[reportData.mno,reportData.iptsp].filter(Boolean);
    if(!sources.length){
        $("dashTotal").textContent="0";
        $("dashSuccess").textContent="0";
        $("dashErrors").textContent="0";
        $("dashErrorPct").textContent="0.00%";
        $("dashboardErrorDetails").textContent="Upload and generate a CSV report to see error statistics.";
        updateDashboardStatus(0,null);
        return;
    }

    let total=0,success=0,errors=0;
    const combined={};
    sources.forEach(data=>{
        total+=data.total;
        success+=data.success;
        errors+=data.errors;
        data.counts.filter(x=>x.code!=="1000").forEach(x=>{
            combined[x.code]=(combined[x.code]||0)+x.count;
        });
    });

    const errorPct=total?errors/total*100:0;
    $("dashTotal").textContent=total.toLocaleString();
    $("dashSuccess").textContent=success.toLocaleString();
    $("dashErrors").textContent=errors.toLocaleString();
    $("dashErrorPct").textContent=errorPct.toFixed(2)+"%";

    const highest=Object.entries(combined).sort((a,b)=>b[1]-a[1])[0];
    if(highest){
        const code=highest[0],count=highest[1];
        const description=DLR_ERROR_DESCRIPTIONS[code]||"Unknown Error Code";
        const pct=total?(count/total*100).toFixed(2):"0.00";
        $("dashboardErrorDetails").innerHTML=
            "<strong>Highest Error Code:</strong> "+escapeHTML(code)+" – "+escapeHTML(description)+"<br>"+
            "<strong>Error Count:</strong> "+count.toLocaleString()+"<br>"+
            "<strong>Error Percentage:</strong> "+pct+"%";
    }else{
        $("dashboardErrorDetails").innerHTML="<strong>No error codes found.</strong>";
    }
    updateDashboardStatus(errorPct,highest);
}

/* AUTOMATIC DASHBOARD STATUS */
function updateDashboardStatus(errorPct,highest){
    const threshold=Math.max(0,Number($("errorThreshold").value)||5);
    const manual=$("reportStatus").value.trim()||"Normal";
    let status="Normal";

    if(errorPct>0&&errorPct>=threshold)status="Warning";
    if(errorPct>0&&errorPct>=threshold*2)status="Critical";

    const badge=$("dashboardStatus");
    badge.textContent=status.toUpperCase();
    badge.className="status-pill";
    if(status==="Warning")badge.classList.add("warning");
    if(status==="Critical")badge.classList.add("critical");

    // The editable report status remains separate from the automatic alert.
    // Both values are visible: automatic health status and manually entered report status.
    badge.title="Automatic status based on error percentage";
}

/* LOGO UPLOAD */
$("logo").addEventListener("change",function(){
    const file=this.files[0];
    if(!file)return;
    if(!file.type.startsWith("image/")){alert("Please select a valid image file.");return;}
    const reader=new FileReader();
    reader.onload=e=>{
        logoData=e.target.result;
        ["mnoLogo","iptspLogo"].forEach(id=>{
            $(id).src=logoData;
            $(id).style.display="block";
        });
    };
    reader.readAsDataURL(file);
});

/* CREATE CANVAS */
async function createReportCanvas(type){
    if(!reportData[type])throw new Error("Please generate the "+type.toUpperCase()+" report first.");
    updateReportInformation();
    return await html2canvas($(type+"Report"),{scale:2,backgroundColor:"#ffffff",useCORS:true});
}

/* PNG / JPG */
async function downloadImage(type,format){
    try{
        const canvas=await createReportCanvas(type);
        const link=document.createElement("a");
        link.download=type.toUpperCase()+"-DLR-Report."+format;
        link.href=canvas.toDataURL(format==="jpg"?"image/jpeg":"image/png",0.95);
        link.click();
    }catch(error){alert(error.message);}
}

/* PDF */
async function downloadPDF(type){
    try{
        const canvas=await createReportCanvas(type);
        const {jsPDF}=window.jspdf;
        const pdf=new jsPDF("p","mm","a4");
        const pageWidth=190,pageHeight=277;
        const imageHeight=canvas.height*pageWidth/canvas.width;
        const imageData=canvas.toDataURL("image/png");

        if(imageHeight<=pageHeight){
            pdf.addImage(imageData,"PNG",10,10,pageWidth,imageHeight);
        }else{
            let remaining=imageHeight,position=0;
            while(remaining>0){
                pdf.addImage(imageData,"PNG",10,10-position,pageWidth,imageHeight);
                remaining-=pageHeight;
                position+=pageHeight;
                if(remaining>0)pdf.addPage();
            }
        }
        pdf.save(type.toUpperCase()+"-DLR-Report.pdf");
    }catch(error){alert(error.message);}
}

/* SUMMARY CSV */
function downloadCSV(type){
    const data=reportData[type];
    if(!data){alert("Please generate the report first.");return;}
    const rows=[["Status Code","Error Description","Count","Percentage"]];
    data.counts.forEach(item=>{
        rows.push([item.code,item.description,item.count,(item.count/data.total*100).toFixed(2)+"%"]);
    });
    rows.push([]);
    rows.push(["Total",data.total]);
    rows.push(["Success",data.success]);
    rows.push(["Error",data.errors]);
    rows.push(["Reporter",getSelectedReporter()]);
    rows.push(["Report Status",$("reportStatus").value.trim()||"Normal"]);
    rows.push(["Monitoring Start",formatTimestamp(data.start)]);
    rows.push(["Monitoring End",formatTimestamp(data.end)]);
    const csv=rows.map(row=>row.map(value=>'"'+String(value??"").replace(/"/g,'""')+'"').join(",")).join("\r\n");
    const blob=new Blob(["\uFEFF"+csv],{type:"text/csv;charset=utf-8"});
    const url=URL.createObjectURL(blob);
    const link=document.createElement("a");
    link.href=url;
    link.download=type.toUpperCase()+"-DLR-Summary.csv";
    link.click();
    setTimeout(()=>URL.revokeObjectURL(url),1000);
}

/* COPY IMAGE */
async function copyImage(type){
    try{
        const canvas=await createReportCanvas(type);
        if(!navigator.clipboard||!window.ClipboardItem)throw new Error("Image copy requires HTTPS or localhost.");
        const blob=await new Promise(resolve=>canvas.toBlob(resolve,"image/png"));
        if(!blob)throw new Error("Could not create report image.");
        await navigator.clipboard.write([new ClipboardItem({"image/png":blob})]);
        alert("Report image copied successfully.");
    }catch(error){alert(error.message);}
}

/* INITIALIZE */
loadSettings();
refreshDashboard();
updateReportInformation();
</script>
</body>
</html>
