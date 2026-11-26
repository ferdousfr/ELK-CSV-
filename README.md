
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>ELK Smart DLR Report Generator</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.4.1/papaparse.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
body{font-family:Arial;background:#f1f5f9;margin:0;color:#172033}
.wrap{max-width:1000px;margin:25px auto;padding:15px}
.card{background:white;padding:20px;margin-bottom:18px;border-radius:12px;box-shadow:0 3px 12px #0001}
h1{background:#17365d;color:white;padding:22px;border-radius:12px}
h2{color:#17365d}
input{padding:10px;border:1px solid #ccd5e0;border-radius:6px;width:100%;margin:8px 0 15px;box-sizing:border-box}
button{padding:11px 17px;border:0;border-radius:6px;background:#2563eb;color:white;cursor:pointer;margin:4px}
button:disabled{opacity:.5}
.report{background:white;padding:25px}
.meta{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:15px 0}
table{width:100%;border-collapse:collapse;margin:12px 0 25px;font-size:14px}
th,td{border:1px solid #d5deea;padding:10px;text-align:left}
th{background:#e8eff8}
td:last-child,th:last-child{text-align:right}
.section{margin-top:25px}
.small{color:#64748b;font-size:12px}
@media(max-width:600px){.meta{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="wrap">
<h1>ELK Smart DLR Report Generator</h1>

<div class="card">
<h2>Report Settings</h2>
<label>Report Entered By</label>
<input id="enteredBy" placeholder="Enter your name">

<label>Optional Logo / Picture</label>
<input id="logo" type="file" accept="image/*">
</div>

<div class="card">
<h2>Upload CSV Files</h2>
<label>DLR MNO CSV</label>
<input id="mnoFile" type="file" accept=".csv">

<label>DLR IPTSP CSV</label>
<input id="iptspFile" type="file" accept=".csv">

<button onclick="generate()">Generate Report</button>
<button onclick="resetAll()">Reset</button>
<p id="msg"></p>
</div>

<div class="card">
<h2>Download Report</h2>
<button id="pngBtn" onclick="downloadPNG()" disabled>Download PNG</button>
<button id="pdfBtn" onclick="downloadPDF()" disabled>Download PDF</button>
<button id="mnoBtn" onclick="downloadCSV('MNO')" disabled>MNO CSV</button>
<button id="iptspBtn" onclick="downloadCSV('IPTSP')" disabled>IPTSP CSV</button>
</div>

<div class="card">
<h2>Report Preview</h2>
<div id="report" class="report">Upload CSV file and generate report.</div>
</div>
</div>

<script>
let data={MNO:[],IPTSP:[]};
let reportNames={MNO:'',IPTSP:''};
let reportTimes={MNO:null,IPTSP:null};
let logoData='';

function key(s){
 return String(s||'').toLowerCase().replace(/[^a-z0-9]/g,'');
}

function field(row,names){
 const keys=Object.keys(row||{});
 for(const name of names){
  const found=keys.find(k=>key(k)===key(name));
  if(found!==undefined && row[found]!=='' && row[found]!=null)
   return row[found];
 }
 return '';
}

function getTimestamp(row){
 return field(row,['@timestamp','timestamp','time','datetime','dateTime','createdAt','eventTime']);
}

function getStatus(row){
 let v=field(row,['statusCode','status_code','status code','errorCode','error_code','responseCode','response_code','code']);
 if(v!=='') return String(v).trim();

 let msg=String(field(row,['message','log','event.original'])||'');
 let m=msg.match(/["']?(?:statusCode|status_code|errorCode|responseCode)["']?\s*[:=]\s*["']?([0-9A-Za-z_-]+)/i);
 return m?m[1]:'Unknown';
}

function getDescription(row){
 let v=field(row,['errorDescription','description','error_description','reason','statusDescription']);
 if(v!=='') return String(v).trim();

 let msg=String(field(row,['message','log','event.original'])||'');
 let m=msg.match(/["']?errordescription["']?\s*[:=]\s*["']([^"']*)/i);
 if(m) return m[1].trim();

 let m2=msg.match(/(?:error\s*description|description)\s*[:=]\s*([^,;}\]]+)/i);
 return m2?m2[1].replace(/^["']|["']$/g,'').trim():'Not Available';
}

function validDate(v){
 if(v===undefined||v===null||v==='')return null;
 let d=new Date(v);
 return isNaN(d.getTime())?null:d;
}

function formatDate(d){
 return d?d.toLocaleString():'Not Available';
}

function parseFile(file){
 return new Promise((resolve,reject)=>{
  Papa.parse(file,{
   header:true,skipEmptyLines:true,
   complete:r=>resolve(r.data||[]),
   error:e=>reject(e)
  });
 });
}

function summarize(rows){
 let groups={};
 let dates=[];

 rows.forEach(row=>{
  let status=getStatus(row);
  let desc=getDescription(row);
  let k=status+'|||'+desc;
  groups[k]=(groups[k]||0)+1;

  let d=validDate(getTimestamp(row));
  if(d)dates.push(d);
 });

 let summary=Object.entries(groups).map(([k,count])=>{
  let p=k.split('|||');
  return {status:p[0],description:p.slice(1).join('|||'),count};
 });

 summary.sort((a,b)=>a.status.localeCompare(b.status,undefined,{numeric:true}));

 dates.sort((a,b)=>a-b);
 return {
  summary,
  start:dates.length?dates[0]:null,
  end:dates.length?dates[dates.length-1]:null
 };
}

async function generate(){
 let mno=document.getElementById('mnoFile').files[0];
 let iptsp=document.getElementById('iptspFile').files[0];

 if(!mno&&!iptsp){
  document.getElementById('msg').textContent='Please upload a CSV file.';
  return;
 }

 try{
  data={MNO:[],IPTSP:[]};
  reportNames={MNO:'',IPTSP:''};
  reportTimes={MNO:null,IPTSP:null};

  if(mno){
   let result=summarize(await parseFile(mno));
   data.MNO=result.summary;
   reportNames.MNO=mno.name.replace(/\.csv$/i,'');
   reportTimes.MNO={start:result.start,end:result.end};
  }

  if(iptsp){
   let result=summarize(await parseFile(iptsp));
   data.IPTSP=result.summary;
   reportNames.IPTSP=iptsp.name.replace(/\.csv$/i,'');
   reportTimes.IPTSP={start:result.start,end:result.end};
  }

  render();
  document.getElementById('msg').textContent='Report generated successfully.';
  document.getElementById('pngBtn').disabled=false;
  document.getElementById('pdfBtn').disabled=false;
  document.getElementById('mnoBtn').disabled=!mno;
  document.getElementById('iptspBtn').disabled=!iptsp;
 }catch(e){
  document.getElementById('msg').textContent='Error: '+e.message;
 }
}

function esc(s){
 return String(s??'').replace(/[&<>"']/g,c=>({
  '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'
 }[c]));
}

function makeSection(type){
 let items=data[type];
 if(!items.length)return '';

 let total=items.reduce((s,x)=>s+x.count,0);
 return `
 <div class="section">
 <h3>${type==='MNO'?'DLR MNO':'DLR IPTSP'}</h3>
 <div><b>Report Title:</b> ${esc(reportNames[type])}</div>
 <div class="meta">
 <div><b>Start Time:</b> ${formatDate(reportTimes[type]?.start)}</div>
 <div><b>End Time:</b> ${formatDate(reportTimes[type]?.end)}</div>
 </div>
 <table>
 <thead><tr><th>Status Code</th><th>Description</th><th>Count</th></tr></thead>
 <tbody>
 ${items.map(x=>`<tr><td>${esc(x.status)}</td><td>${esc(x.description)}</td><td>${x.count}</td></tr>`).join('')}
 <tr><th colspan="2">Total Records</th><th>${total}</th></tr>
 </tbody>
 </table>
 </div>`;
}

function render(){
 let entered=esc(document.getElementById('enteredBy').value||'Not Provided');
 let logo=logoData?`<img src="${logoData}" style="max-width:100px;max-height:75px;object-fit:contain">`:'';

 document.getElementById('report').innerHTML=`
 <div id="reportContent">
 <div style="display:flex;align-items:center;gap:18px;border-bottom:2px solid #dce5f0;padding-bottom:15px">
 ${logo}
 <div>
 <h2>ELK DLR Summary Report</h2>
 <div><b>Report Entered By:</b> ${entered}</div>
 <div><b>Report Generated:</b> ${new Date().toLocaleString()}</div>
 </div>
 </div>
 ${makeSection('MNO')}
 ${makeSection('IPTSP')}
 <p class="small" style="text-align:right;border-top:1px solid #ddd;padding-top:12px">ELK Smart DLR Report Generator</p>
 </div>`;
}

document.getElementById('logo').addEventListener('change',e=>{
 let f=e.target.files[0];
 if(!f)return;
 let r=new FileReader();
 r.onload=()=>{logoData=r.result;if(data.MNO.length||data.IPTSP.length)render();};
 r.readAsDataURL(f);
});

document.getElementById('enteredBy').addEventListener('change',()=>{
 if(data.MNO.length||data.IPTSP.length)render();
});

async function downloadPNG(){
 let el=document.getElementById('reportContent');
 if(!el)return;
 let canvas=await html2canvas(el,{scale:2,backgroundColor:'#fff'});
 let a=document.createElement('a');
 a.download='ELK_DLR_Report.png';
 a.href=canvas.toDataURL('image/png');
 a.click();
}

async function downloadPDF(){
 let el=document.getElementById('reportContent');
 if(!el)return;
 let canvas=await html2canvas(el,{scale:2,backgroundColor:'#fff'});
 let pdf=new jspdf.jsPDF('p','mm','a4');
 let w=pdf.internal.pageSize.getWidth();
 let h=canvas.height*w/canvas.width;
 let pageH=pdf.internal.pageSize.getHeight();
 let img=canvas.toDataURL('image/png');
 let y=0,remaining=h;
 while(remaining>0){
  if(y!==0)pdf.addPage();
  pdf.addImage(img,'PNG',0,y,w,h);
  remaining-=pageH;
  y-=pageH;
 }
 pdf.save('ELK_DLR_Report.pdf');
}

function downloadCSV(type){
 let items=data[type];
 if(!items.length)return;
 let rows=[['Status Code','Description','Count'],...items.map(x=>[x.status,x.description,x.count])];
 let csv=rows.map(r=>r.map(v=>'"'+String(v).replace(/"/g,'""')+'"').join(',')).join('\r\n');
 let blob=new Blob(['\ufeff'+csv],{type:'text/csv;charset=utf-8'});
 let a=document.createElement('a');
 a.href=URL.createObjectURL(blob);
 a.download=reportNames[type]+'.csv';
 a.click();
 URL.revokeObjectURL(a.href);
}

function resetAll(){
 location.reload();
}
</script>
</body>
</html>
