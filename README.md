
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
    --primary: #5146e5;
    --dark: #202b45;
    --muted: #718096;
    --border: #e1e7f0;
    --background: #f5f7fc;
    --success: #16834a;
    --danger: #d04444;
}

* { box-sizing: border-box; }

body {
    margin: 0;
    background: var(--background);
    color: var(--dark);
    font-family: Arial, sans-serif;
    font-size: 14px;
}

button, input { font: inherit; }

.app {
    display: flex;
    min-height: 100vh;
}

.sidebar {
    width: 220px;
    background: #fff;
    border-right: 1px solid var(--border);
    padding: 24px 14px;
    flex-shrink: 0;
}

.brand {
    color: #214c80;
    font-size: 19px;
    font-weight: 800;
    line-height: 1.4;
    margin: 0 10px 35px;
}

.nav {
    padding: 13px 12px;
    border-radius: 8px;
    margin-bottom: 5px;
    color: #586780;
}

.nav.active {
    background: #f0efff;
    color: var(--primary);
    font-weight: bold;
}

.main {
    flex: 1;
    min-width: 0;
}

.topbar {
    background: white;
    border-bottom: 1px solid var(--border);
    padding: 18px 25px;
    display: flex;
    justify-content: space-between;
    gap: 12px;
    flex-wrap: wrap;
}

.tabs {
    background: white;
    border-bottom: 1px solid var(--border);
    display: flex;
    gap: 25px;
    padding: 15px 25px;
    overflow-x: auto;
}

.tabs span {
    white-space: nowrap;
    color: #65728a;
}

.tabs .active {
    color: var(--primary);
    font-weight: bold;
    border-bottom: 2px solid var(--primary);
    padding-bottom: 10px;
}

.content {
    max-width: 1250px;
    margin: auto;
    padding: 25px;
}

.page-title {
    font-size: 25px;
    margin: 0 0 22px;
}

.card {
    background: white;
    border: 1px solid var(--border);
    border-radius: 12px;
    margin-bottom: 20px;
    overflow: hidden;
    box-shadow: 0 3px 12px rgba(30,50,90,.035);
}

.card-title {
    padding: 17px 22px;
    border-bottom: 1px solid #edf0f5;
    font-weight: bold;
    font-size: 15px;
}

.card-body {
    padding: 22px;
}

.grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 18px;
}

.field label {
    display: block;
    margin-bottom: 8px;
    color: var(--muted);
    font-size: 12px;
    font-weight: bold;
}

.field input {
    width: 100%;
    padding: 12px;
    border: 1px solid #ccd5e4;
    border-radius: 7px;
    background: white;
}

.upload-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 18px;
}

.upload-box {
    text-align: center;
    padding: 25px 18px;
    border: 1px dashed #bdc9dd;
    border-radius: 10px;
    background: #fbfcff;
}

.upload-box h3 {
    margin: 0 0 10px;
}

.upload-box input {
    width: 100%;
    margin-top: 12px;
}

.file-status {
    color: var(--muted);
    font-size: 12px;
    margin-top: 12px;
    overflow-wrap: anywhere;
}

.btn {
    padding: 11px 16px;
    border: none;
    border-radius: 7px;
    background: var(--primary);
    color: white;
    font-weight: bold;
    cursor: pointer;
}

.btn:hover { opacity: .88; }

.btn.secondary {
    background: #edf0f7;
    color: #34425e;
}

.btn.danger {
    background: #fff0f0;
    color: #bd3535;
}

.actions {
    display: flex;
    flex-wrap: wrap;
    gap: 9px;
    margin-top: 15px;
}

.status-message {
    color: var(--muted);
    margin: 15px 0 0;
    line-height: 1.5;
}

.report {
    background: white;
    color: #1c2433;
    padding: 32px;
    border: 1px solid #e0e5ed;
}

.report-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 15px;
    margin-bottom: 25px;
}

.report-logo {
    max-width: 180px;
    max-height: 55px;
    object-fit: contain;
}

.report-company {
    color: #63718a;
    font-size: 12px;
    letter-spacing: 1.5px;
    font-weight: bold;
}

.report h2 {
    font-family: Georgia, serif;
    font-size: 34px;
    font-weight: normal;
    margin: 0 0 10px;
}

.period {
    color: #77839a;
    font-size: 14px;
    margin-bottom: 25px;
    overflow-wrap: anywhere;
}

.summary {
    display: flex;
    flex-wrap: wrap;
    gap: 28px;
    margin: 22px 0;
    font-family: monospace;
    font-size: 16px;
}

.summary strong { color: #1d2d4b; }

.report table {
    width: 100%;
    border-collapse: collapse;
    font-family: monospace;
}

.report th,
.report td {
    padding: 12px;
    border: 1px solid #d8deea;
    text-align: left;
}

.report th {
    background: #edf1f7;
    font-weight: bold;
}

.report td:last-child,
.report th:last-child {
    text-align: right;
}

.report-meta {
    margin-top: 28px;
    font-family: monospace;
    font-weight: bold;
    line-height: 2;
}

.report-status {
    color: var(--success);
}

.empty-row {
    text-align: center !important;
    color: #8993a5;
}

.small-note {
    color: var(--muted);
    font-size: 12px;
    line-height: 1.6;
}

@media(max-width:850px) {
    .sidebar { display: none; }
    .content { padding: 14px; }
    .grid, .upload-grid { grid-template-columns: 1fr; }
    .report { padding: 18px; }
    .report h2 { font-size: 25px; }
    .report th, .report td {
        padding: 8px 5px;
        font-size: 11px;
    }
    .summary { gap: 13px; font-size: 13px; }
}
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
            <div>
                <span id="clock12"></span> |
                <span id="clock24"></span>
            </div>
        </header>

        <div class="tabs">
            <span>9xxx Report</span>
            <span>1xxx Report</span>
            <span>4xx/5xx Report</span>
            <span class="active">DLR Report</span>
            <span>Delay Report</span>
        </div>

        <main class="content">

            <h1 class="page-title">
                DLR <span style="color:#5146e5">Report Generator</span>
            </h1>

            <!-- Monitoring Window -->
            <section class="card">
                <div class="card-title">Monitoring Window</div>
                <div class="card-body">
                    <strong id="monitoringInfo">Not generated yet</strong>
                    <p class="small-note">
                        Monitoring window is automatically calculated
                        from the earliest and latest values in the
                        CSV @timestamp column.
                    </p>
                </div>
            </section>

            <!-- Report Information -->
            <section class="card">
                <div class="card-title">Report Information</div>
                <div class="card-body grid">

                    <div class="field">
                        <label>Reporter Name</label>
                        <input id="reporter"
                               list="reporterList"
                               placeholder="Enter reporter name">
                        <datalist id="reporterList"></datalist>
                    </div>

                    <div class="field">
                        <label>Company Logo (Optional)</label>
                        <input type="file" id="logo" accept="image/*">
                    </div>

                </div>
            </section>

            <!-- CSV Upload -->
            <section class="card">
                <div class="card-title">Upload DLR CSV Files</div>

                <div class="card-body upload-grid">

                    <div class="upload-box">
                        <h3>📁 DLR MNO</h3>
                        <p class="small-note">Upload MNO CSV file</p>
                        <input type="file" id="mnoFile" accept=".csv">
                        <div class="file-status" id="mnoFileStatus">
                            No file selected
                        </div>
                    </div>

                    <div class="upload-box">
                        <h3>📁 DLR IPTSP</h3>
                        <p class="small-note">Upload IPTSP CSV file</p>
                        <input type="file" id="iptspFile" accept=".csv">
                        <div class="file-status" id="iptspFileStatus">
                            No file selected
                        </div>
                    </div>

                </div>
            </section>

            <!-- Generate -->
            <section class="card">
                <div class="card-title">Generate and Export Reports</div>

                <div class="card-body">

                    <div class="actions">
                        <button class="btn" onclick="generateReport('mno')">
                            Generate MNO Report
                        </button>

                        <button class="btn" onclick="generateReport('iptsp')">
                            Generate IPTSP Report
                        </button>
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

                    <p id="message" class="status-message">
                        Upload a CSV file to generate a report.
                    </p>

                </div>
            </section>

            <!-- MNO Preview -->
            <section class="card">
                <div class="card-title">DLR MNO Report Preview</div>
                <div class="card-body">

                    <div class="report" id="mnoReport">
                        <div class="report-header">
                            <div class="report-company">
                                INFOZILLION TELETECH BD<br>
                                SERVICE ASSURANCE
                            </div>
                            <img class="report-logo"
                                 id="mnoLogo"
                                 alt=""
                                 style="display:none">
                        </div>

                        <h2>DLR Report — MNO</h2>
                        <div class="period" id="mnoPeriod">
                            Monitoring Window: Not available
                        </div>

                        <div class="summary">
                            <span>Total: <strong id="mnoTotal">0</strong></span>
                            <span>Success: <strong id="mnoSuccess">0</strong></span>
                            <span>Error: <strong id="mnoErrors">0</strong></span>
                        </div>

                        <table>
                            <thead>
                                <tr>
                                    <th>Status Code</th>
                                    <th>Error Description</th>
                                    <th>Count</th>
                                </tr>
                            </thead>
                            <tbody id="mnoRows">
                                <tr><td colspan="3" class="empty-row">No data loaded</td></tr>
                            </tbody>
                        </table>

                        <div class="report-meta">
                            Reporter: <span class="reporter-name">Not specified</span><br>
                            Status: <span class="report-status">Normal</span>
                        </div>
                    </div>

                </div>
            </section>

            <!-- IPTSP Preview -->
            <section class="card">
                <div class="card-title">DLR IPTSP Report Preview</div>
                <div class="card-body">

                    <div class="report" id="iptspReport">
                        <div class="report-header">
                            <div class="report-company">
                                INFOZILLION TELETECH BD<br>
                                SERVICE ASSURANCE
                            </div>
                            <img class="report-logo"
                                 id="iptspLogo"
                                 alt=""
                                 style="display:none">
                        </div>

                        <h2>DLR Report — IPTSP</h2>
                        <div class="period" id="iptspPeriod">
                            Monitoring Window: Not available
                        </div>

                        <div class="summary">
                            <span>Total: <strong id="iptspTotal">0</strong></span>
                            <span>Success: <strong id="iptspSuccess">0</strong></span>
                            <span>Error: <strong id="iptspErrors">0</strong></span>
                        </div>

                        <table>
                            <thead>
                                <tr>
                                    <th>Status Code</th>
                                    <th>Error Description</th>
                                    <th>Count</th>
                                </tr>
                            </thead>
                            <tbody id="iptspRows">
                                <tr><td colspan="3" class="empty-row">No data loaded</td></tr>
                            </tbody>
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

/* ==========================================
   1. OFFICIAL ERROR CODE MAPPING
   This is the ONLY source for descriptions.
========================================== */

const DLR_ERROR_DESCRIPTIONS = {
    "1000": "Success",
    "1001": "IP Blacklist",
    "1002": "Invalid Username",
    "1003": "Invalid Password",
    "1004": "Parameter missing",
    "1005": "Invalid Parameter",
    "1006": "CLI/Masking Invalid",
    "1007": "Account Barred",
    "1008": "Insufficient Balance",
    "1009": "DND User",
    "1010": "Invalid MSISDN",
    "1011": "Duplicate Transaction ID",
    "1012": "Message lengths exceed",
    "1013": "No Request found",
    "1014": "Delivery pending",
    "1015": "TPS Limit Exceeded",
    "1016": "Number Barred",
    "1017": "API is not allowed for user",
    "1018": "No Live Campaign",
    "1019": "Messagebody Invalid",
    "1020": "Internal Server Error",
    "1021": "CLI/Masking Already Exists",
    "1050": "Allowed campaigns limit exceeded",
    "1051": "Allowed SMS quota is completed",
    "1052": "Submission record not found",
    "1053": "Invalid Transaction Id",
    "1054": "MSISDN Limit Exceeded"
};


/* ==========================================
   2. BANGLADESH CLOCK
========================================== */

function updateClock() {
    const now = new Date();

    const options = {
        timeZone: "Asia/Dhaka",
        hour: "2-digit",
        minute: "2-digit",
        second: "2-digit"
    };

    document.getElementById("clock12").textContent =
        new Intl.DateTimeFormat("en-US", {
            ...options,
            hour12: true
        }).format(now);

    document.getElementById("clock24").textContent =
        new Intl.DateTimeFormat("en-GB", {
            ...options,
            hour12: false
        }).format(now);
}

updateClock();
setInterval(updateClock, 1000);


/* ==========================================
   3. REPORTER NAME SAVING
========================================== */

const reporterInput = document.getElementById("reporter");

function loadReporterNames() {
    const names = JSON.parse(
        localStorage.getItem("dlrReporterNames") || "[]"
    );

    const list = document.getElementById("reporterList");
    list.innerHTML = "";

    names.forEach(name => {
        const option = document.createElement("option");
        option.value = name;
        list.appendChild(option);
    });
}

reporterInput.addEventListener("change", function() {
    const name = this.value.trim();
    if (!name) return;

    const names = JSON.parse(
        localStorage.getItem("dlrReporterNames") || "[]"
    );

    if (!names.includes(name)) {
        names.push(name);
        localStorage.setItem(
            "dlrReporterNames",
            JSON.stringify(names)
        );
    }

    loadReporterNames();
});

loadReporterNames();


/* ==========================================
   4. CSV PARSER
========================================== */

function parseCSV(text) {
    text = text.replace(/^\uFEFF/, "");

    const firstLine = text.split(/\r?\n/)[0] || "";
    const delimiters = [",", ";", "\t", "|"];

    const delimiter = delimiters.reduce((best, current) => {
        return firstLine.split(current).length >
               firstLine.split(best).length
            ? current
            : best;
    }, ",");

    const rows = [];
    let row = [];
    let cell = "";
    let quoted = false;

    for (let i = 0; i < text.length; i++) {
        const char = text[i];

        if (char === '"' && quoted && text[i + 1] === '"') {
            cell += '"';
            i++;
        } else if (char === '"') {
            quoted = !quoted;
        } else if (char === delimiter && !quoted) {
            row.push(cell);
            cell = "";
        } else if ((char === "\n" || char === "\r") && !quoted) {
            if (char === "\r" && text[i + 1] === "\n") i++;

            row.push(cell);

            if (row.some(value => value.trim() !== "")) {
                rows.push(row);
            }

            row = [];
            cell = "";
        } else {
            cell += char;
        }
    }

    row.push(cell);

    if (row.some(value => value.trim() !== "")) {
        rows.push(row);
    }

    return rows;
}


/* ==========================================
   5. FIND CSV COLUMN
========================================== */

function findColumn(headers, possibleNames) {
    return headers.findIndex(header =>
        possibleNames.includes(
            header.toLowerCase().trim()
        )
    );
}


/* ==========================================
   6. EXTRACT STATUS CODE
========================================== */

function extractStatusCode(row, headers, messageIndex) {

    /*
       First priority:
       A separate Status Code column.
    */

    const statusIndex = findColumn(headers, [
        "statuscode",
        "status_code",
        "status code",
        "errorcode",
        "error_code",
        "error code",
        "responsecode",
        "response_code",
        "response code"
    ]);

    if (statusIndex >= 0) {
        const value = (row[statusIndex] || "").trim();

        if (/^\d{3,5}$/.test(value)) {
            return value;
        }
    }

    /*
       Second priority:
       Extract code from the message column.
    */

    const message = messageIndex >= 0
        ? (row[messageIndex] || "").trim()
        : "";

    if (!message) return "Unknown";

    const patterns = [
        /"(?:statusCode|status_code|errorCode|error_code|responseCode|response_code|code|status)"\s*:\s*["']?(\d{3,5})/i,

        /(?:statusCode|status_code|errorCode|error_code|responseCode|response_code|code|status)\s*[=:]\s*["']?(\d{3,5})/i,

        /^\s*(\d{3,5})(?:\s*[:\-]|$)/,

        /(?:HTTP|http)\s+(\d{3,5})\b/
    ];

    for (const pattern of patterns) {
        const match = message.match(pattern);

        if (match) {
            return match[1];
        }
    }

    /*
       If no valid code is found,
       do not guess from arbitrary numbers.
    */

    return "Unknown";
}


/* ==========================================
   7. TIMESTAMP PARSER
========================================== */

function parseTimestamp(value) {
    if (!value) return null;

    value = value.trim();

    const match = value.match(
        /^([A-Za-z]{3})\s+(\d{1,2}),\s*(\d{4})\s*@\s*(\d{1,2}):(\d{2}):(\d{2})(?:\.(\d{1,3}))?$/
    );

    if (match) {
        const months = {
            Jan: 0, Feb: 1, Mar: 2, Apr: 3,
            May: 4, Jun: 5, Jul: 6, Aug: 7,
            Sep: 8, Oct: 9, Nov: 10, Dec: 11
        };

        return new Date(
            Number(match[3]),
            months[match[1]],
            Number(match[2]),
            Number(match[4]),
            Number(match[5]),
            Number(match[6]),
            Number((match[7] || "0").padEnd(3, "0"))
        );
    }

    const parsed = new Date(value);

    return isNaN(parsed.getTime()) ? null : parsed;
}


/* ==========================================
   8. TIMESTAMP DISPLAY FORMAT
========================================== */

function formatTimestamp(date) {
    const month = date.toLocaleString("en-US", {
        month: "short"
    });

    const day = String(date.getDate()).padStart(2, "0");
    const year = date.getFullYear();

    const hours = String(date.getHours()).padStart(2, "0");
    const minutes = String(date.getMinutes()).padStart(2, "0");
    const seconds = String(date.getSeconds()).padStart(2, "0");
    const milliseconds = String(date.getMilliseconds()).padStart(3, "0");

    return `${month} ${day}, ${year} @ ${hours}:${minutes}:${seconds}.${milliseconds}`;
}


/* ==========================================
   9. ANALYZE CSV
========================================== */

function analyzeCSV(text) {
    const rows = parseCSV(text);

    if (rows.length < 2) {
        throw new Error("CSV file has no data rows.");
    }

    const headers = rows[0].map(header =>
        header.trim().toLowerCase()
    );

    const messageIndex = findColumn(headers, [
        "message",
        "response",
        "responsemessage",
        "response_message"
    ]);

    const timestampIndex = findColumn(headers, [
        "@timestamp"
    ]);

    if (timestampIndex < 0) {
        throw new Error(
            'The CSV file must contain an "@timestamp" column.'
        );
    }

    const counts = {};
    const timestamps = [];

    for (let i = 1; i < rows.length; i++) {
        const row = rows[i];

        if (!row || row.every(value => !value.trim())) {
            continue;
        }

        const code = extractStatusCode(
            row,
            headers,
            messageIndex
        );

        /*
           IMPORTANT:
           Description comes ONLY from official mapping.
           No message text is used as a description.
        */

        const description =
            DLR_ERROR_DESCRIPTIONS[code] ||
            "Unknown Error Code";

        if (!counts[code]) {
            counts[code] = {
                code: code,
                description: description,
                count: 0
            };
        }

        counts[code].count++;

        const timestamp = parseTimestamp(
            row[timestampIndex]
        );

        if (timestamp) {
            timestamps.push(timestamp);
        }
    }

    if (!Object.keys(counts).length) {
        throw new Error("No valid records found in CSV.");
    }

    if (!timestamps.length) {
        throw new Error(
            'No valid timestamps found in "@timestamp".'
        );
    }

    timestamps.sort(
        (a, b) => a.getTime() - b.getTime()
    );

    return {
        counts: Object.values(counts),
        total: Object.values(counts).reduce(
            (sum, item) => sum + item.count,
            0
        ),
        success: counts["1000"]
            ? counts["1000"].count
            : 0,
        start: timestamps[0],
        end: timestamps[timestamps.length - 1]
    };
}


/* ==========================================
   10. GENERATE REPORT
========================================== */

const reportData = {
    mno: null,
    iptsp: null
};

async function generateReport(type) {
    const fileInput = document.getElementById(
        type === "mno" ? "mnoFile" : "iptspFile"
    );

    const message = document.getElementById("message");

    try {
        if (!fileInput.files.length) {
            throw new Error(
                "Please select the " +
                type.toUpperCase() +
                " CSV file first."
            );
        }

        message.textContent = "Processing CSV file...";

        const text = await fileInput.files[0].text();
        const result = analyzeCSV(text);

        reportData[type] = result;

        renderReport(type, result);

        message.textContent =
            type.toUpperCase() +
            " report generated successfully.";

    } catch (error) {
        message.textContent = "Error: " + error.message;
    }
}


/* ==========================================
   11. RENDER REPORT
========================================== */

function renderReport(type, data) {
    const tbody = document.getElementById(type + "Rows");
    tbody.innerHTML = "";

    data.counts.sort((a, b) => {
        if (a.code === "1000") return -1;
        if (b.code === "1000") return 1;

        return a.code.localeCompare(
            b.code,
            undefined,
            { numeric: true }
        );
    });

    data.counts.forEach(item => {
        const tr = document.createElement("tr");

        const codeCell = document.createElement("td");
        const descriptionCell = document.createElement("td");
        const countCell = document.createElement("td");

        codeCell.textContent = item.code;
        descriptionCell.textContent = item.description;
        countCell.textContent = item.count.toLocaleString();

        tr.appendChild(codeCell);
        tr.appendChild(descriptionCell);
        tr.appendChild(countCell);

        tbody.appendChild(tr);
    });

    const errors = data.total - data.success;

    document.getElementById(type + "Total").textContent =
        data.total.toLocaleString();

    document.getElementById(type + "Success").textContent =
        data.success.toLocaleString();

    document.getElementById(type + "Errors").textContent =
        errors.toLocaleString();

    const period =
        formatTimestamp(data.start) +
        " - " +
        formatTimestamp(data.end);

    document.getElementById(type + "Period").textContent =
        period;

    document.getElementById("monitoringInfo").textContent =
        period;

    updateReporterName();
}


/* ==========================================
   12. UPDATE REPORTER NAME
========================================== */

function updateReporterName() {
    const name = reporterInput.value.trim() || "Not specified";

    document.querySelectorAll(".reporter-name").forEach(element => {
        element.textContent = name;
    });
}

reporterInput.addEventListener("input", updateReporterName);


/* ==========================================
   13. FILE SELECTION STATUS
========================================== */

["mno", "iptsp"].forEach(type => {
    const input = document.getElementById(type + "File");

    input.addEventListener("change", function() {
        document.getElementById(type + "FileStatus").textContent =
            this.files[0]
                ? this.files[0].name
                : "No file selected";
    });
});


/* ==========================================
   14. COMPANY LOGO
========================================== */

document.getElementById("logo").addEventListener("change", function() {
    const file = this.files[0];

    if (!file) return;

    if (!file.type.startsWith("image/")) {
        alert("Please select a valid image file.");
        return;
    }

    const reader = new FileReader();

    reader.onload = function(event) {
        ["mnoLogo", "iptspLogo"].forEach(id => {
            const image = document.getElementById(id);
            image.src = event.target.result;
            image.style.display = "block";
        });
    };

    reader.readAsDataURL(file);
});


/* ==========================================
   15. CREATE REPORT CANVAS
========================================== */

async function createReportCanvas(type) {
    if (!reportData[type]) {
        throw new Error(
            "Please generate the " +
            type.toUpperCase() +
            " report first."
        );
    }

    return await html2canvas(
        document.getElementById(type + "Report"),
        {
            scale: 2,
            backgroundColor: "#ffffff",
            useCORS: true
        }
    );
}


/* ==========================================
   16. DOWNLOAD PNG / JPG
========================================== */

async function downloadImage(type, format) {
    try {
        const canvas = await createReportCanvas(type);

        const link = document.createElement("a");

        link.download =
            type.toUpperCase() +
            "-DLR-Report." +
            format;

        link.href = canvas.toDataURL(
            format === "jpg"
                ? "image/jpeg"
                : "image/png",
            0.95
        );

        link.click();

    } catch (error) {
        alert(error.message);
    }
}


/* ==========================================
   17. DOWNLOAD PDF
========================================== */

async function downloadPDF(type) {
    try {
        const canvas = await createReportCanvas(type);

        const { jsPDF } = window.jspdf;

        const pdf = new jsPDF("p", "mm", "a4");

        const pageWidth = 190;
        const pageHeight = 277;

        const imageHeight =
            canvas.height * pageWidth / canvas.width;

        const imageData = canvas.toDataURL("image/png");

        if (imageHeight <= pageHeight) {
            pdf.addImage(
                imageData,
                "PNG",
                10,
                10,
                pageWidth,
                imageHeight
            );
        } else {
            let remaining = imageHeight;
            let position = 0;

            while (remaining > 0) {
                pdf.addImage(
                    imageData,
                    "PNG",
                    10,
                    10 - position,
                    pageWidth,
                    imageHeight
                );

                remaining -= pageHeight;
                position += pageHeight;

                if (remaining > 0) {
                    pdf.addPage();
                }
            }
        }

        pdf.save(type.toUpperCase() + "-DLR-Report.pdf");

    } catch (error) {
        alert(error.message);
    }
}


/* ==========================================
   18. DOWNLOAD SUMMARY CSV
========================================== */

function downloadCSV(type) {
    const data = reportData[type];

    if (!data) {
        alert("Please generate the report first.");
        return;
    }

    const rows = [
        ["Status Code", "Error Description", "Count"]
    ];

    data.counts.forEach(item => {
        rows.push([
            item.code,
            item.description,
            item.count
        ]);
    });

    const csv = rows.map(row =>
        row.map(value =>
            '"' + String(value).replace(/"/g, '""') + '"'
        ).join(",")
    ).join("\r\n");

    const blob = new Blob(
        ["\uFEFF" + csv],
        { type: "text/csv;charset=utf-8" }
    );

    const url = URL.createObjectURL(blob);
    const link = document.createElement("a");

    link.href = url;
    link.download = type.toUpperCase() + "-DLR-Summary.csv";

    link.click();

    URL.revokeObjectURL(url);
}


/* ==========================================
   19. COPY REPORT IMAGE
========================================== */

async function copyImage(type) {
    try {
        const canvas = await createReportCanvas(type);

        if (!navigator.clipboard || !window.ClipboardItem) {
            throw new Error(
                "Image copy requires HTTPS or localhost."
            );
        }

        const blob = await new Promise(resolve =>
            canvas.toBlob(resolve, "image/png")
        );

        await navigator.clipboard.write([
            new ClipboardItem({
                "image/png": blob
            })
        ]);

        alert("Report image copied successfully.");

    } catch (error) {
        alert(error.message);
    }
}


/* ==========================================
   20. INITIALIZATION
========================================== */

updateReporterName();

</script>
</body>
</html>
