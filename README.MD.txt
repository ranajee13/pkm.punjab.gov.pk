<!DOCTYPE html> 
<html class="transition-navbar-scroll top-navbar-xlarge bottom-footer" lang="en"> 
<head> 
<meta charset="utf-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1"> 
<title>Document Verification</title>
<!-- CSS (index-assets folder) --> 
<link href="index-assets/css/theme-core.min.css" rel="stylesheet"> 
<link href="index-assets/css/module-essentials.min.css" rel="stylesheet" /> 
<link href="index-assets/css/module-material.min.css" rel="stylesheet" /> 
<link href="index-assets/css/module-layout.min.css" rel="stylesheet" /> 
<link href="index-assets/css/module-navbar.min.css" rel="stylesheet" />
<style> 
body { 
 margin: 0; 
 padding: 0; 
 background-color: #ffffff; 
 font-family: Arial, sans-serif;
} 
#bg-wrapper { 
 background: url("index-assets/images/bg.jpg") no-repeat center top; 
 background-size: cover; 
 width: 100%;
 display: flow-root; 
} 
.top-head { 
 background: #fff; 
 opacity: 0.2; 
 min-height: 85px; 
} 
.navbar { 
 top: -75px; 
 margin-top: 0px; 
 border-bottom: 1px solid #ddd; 
} 
.panel-default { 
 margin-top: -55px; 
 min-height: 500px; 
 box-shadow: 0 4px 15px rgba(0,0,0,0.2); 
 background: #fff;
 border-radius: 4px;
 width: 100%;
}
.form-group label, .captcha-question { 
 display: block;
 text-align: center; 
 width: 100%;
 font-size: 18px;
 font-weight: bold;
 color: #333;
 margin-bottom: 15px;
} 
.form-control {
 width: 100% !important;
 text-align: left;
 margin-bottom: 10px;
}
.captcha-input-container { 
 display: flex; 
 gap: 10px; 
 align-items: center; 
 width: 100%;
} 
.captcha-refresh-button { 
 background: #007bff; 
 color: white; 
 border: none; 
 padding: 6px 15px; 
 border-radius: 4px; 
 cursor: pointer; 
 height: 34px; 
} 
.btn-submit-custom {
 background: #4E62DA; 
 padding: 10px 30px; 
 color: white;
 border: none;
 border-radius: 4px;
 display: inline-block;
}
.footer-blur { 
 background: rgba(255, 255, 255, 0.4); 
 backdrop-filter: blur(10px); 
 -webkit-backdrop-filter: blur(10px); 
 color: #333; 
 text-align: center; 
 padding: 20px 0; 
 width: 100%; 
 font-size: 14px; 
 border-top: 1px solid rgba(255, 255, 255, 0.3);
 margin-top: 50px; 
} 
@media screen and (max-width: 768px) {
 .panel-default { margin-top: -20px; min-height: 450px; }
}
</style> 
</head>
<body class="flat-blue"> 
<div id="bg-wrapper">
 <div class="top-head"></div>
 
 <nav class="navbar navbar-default navbar-size-xlarge paper-shadow"> 
 <div class="container-fluid"> 
 <div class="navbar-brand"> 
 <img src="index-assets/images/logo.png" height="50"> 
 </div> 
 </div> 
 </nav>

 <div class="container-fluid"> 
 <div class="row"> 
 <div class="col-md-12">
 <div class="panel panel-default text-center"> 
 <div class="panel-heading" style="min-height:55px;"> 
 <h2 class="panel-title text-center">Document Verification</h2> 
 </div> 
 <div class="panel-body"> 
 <form id="verificationForm"> 
 <br> 
 <div class="form-group"> 
 <label>CNIC Number (required)</label> 
 <input type="text" id="cnic" class="form-control" placeholder="Enter CNIC No/ e.g 31302-6789890-3" maxlength="15" required> 
 </div> 
 <div class="form-group"> 
 <label id="captchaLabel" class="captcha-question"></label> 
 <div class="captcha-input-container"> 
 <input type="number" id="captchaInput" class="form-control" placeholder="Enter captcha results" required style="flex-grow: 1;"> 
 <button type="button" onclick="generateCaptcha()" class="captcha-refresh-button">Refresh</button> 
 </div> 
 </div> 
 
 <br> 
 <div class="col-md-12 text-center"> 
 <button type="submit" class="btn-submit-custom">Submit</button> 
 </div>
 </form> 
 </div> 
 </div> 
 </div>
 </div> 
 </div>
 <div class="footer-blur"> 
 © Copyright 2026 PITB 
 </div> 
</div> 
<div style="min-height: 200px; background: #fff;"></div>

<script> 
var correctAns; 
var targetCNIC = "31302-4422466-3";

// --- Auto Dash Logic Start ---
document.getElementById('cnic').addEventListener('input', function (e) {
    var value = e.target.value.replace(/\D/g, '');
    var formattedValue = '';
    if (value.length > 0) {
        formattedValue = value.substring(0, 5);
        if (value.length > 5) {
            formattedValue += '-' + value.substring(5, 12);
        }
        if (value.length > 12) {
            formattedValue += '-' + value.substring(12, 13);
        }
    }
    e.target.value = formattedValue;
});
// --- Auto Dash Logic End ---

function generateCaptcha() { 
 var n1 = Math.floor(Math.random() * 10) + 1; 
 var n2 = Math.floor(Math.random() * 10) + 1; 
 correctAns = n1 + n2; 
 document.getElementById('captchaLabel').innerText = n1 + " + " + n2 + " ="; 
 document.getElementById('captchaInput').value = ""; 
}

window.onload = function() { generateCaptcha(); };

document.getElementById('verificationForm').onsubmit = function(e) { 
 e.preventDefault(); 
 var userCnic = document.getElementById('cnic').value.trim(); 
 var userAns = parseInt(document.getElementById('captchaInput').value);
 
 if (userAns !== correctAns) { 
 alert("Incorrect Captcha. Try again."); 
 generateCaptcha(); 
 return; 
 }
 
 if (userCnic === targetCNIC) { 
 window.location.href = "page2.html"; 
 } else { 
 alert("Invalid CNIC! Record not found."); 
 generateCaptcha(); 
 } 
}; 
</script>
</body> 
</html>
