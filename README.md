![h](https://github.com/user-attachments/assets/89d73458-aa5b-4eb1-a2f4-79f11cf1ddf3)# Hammaddev
GPA Calculator by Hammad Developer  A simple yet powerful tool designed to help students quickly and accurately calculate their Grade Point Average. With an intuitive interface, customizable grading scales, and support for multiple courses, this calculator makes academic tracking effortless. 
[index.html](https://github.com/user-attachments/files/25843955/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Master Tags -->
    <title>Smart GPA & CGPA Calculator | Hammad Developer</title>
    <meta name="description" content="Calculate your GPA and CGPA with dynamic scales (80, 85, 90). The most accurate, responsive academic tool for students worldwide. Optimized by Hammad Developer.">
    <meta name="keywords" content="GPA Calculator, CGPA Calculator, 80 marks 4.0 gpa, 85 marks 4.0 gpa, 90 marks 4.0 gpa, Hammad Developer, Academic Tool">
    <meta name="author" content="Hammad Developer">
    <meta name="robots" content="index, follow">

    <!-- JSON-LD for Google Search Ranking -->
    <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "SoftwareApplication",
      "name": "Smart GPA Calculator",
      "operatingSystem": "All",
      "applicationCategory": "EducationApplication",
      "author": { "@type": "Person", "name": "Hammad Developer" }
    }
    </script>

    <!-- Free Tab Icon (Emoji) -->
    <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🎓</text></svg>">
    
    <link href="https://fonts.googleapis.com" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <main class="app-wrapper">
        <!-- Logo & Title -->
        <header class="header">
            <div class="logo-wrapper">
                <svg class="main-svg-logo" viewBox="0 0 24 24" xmlns="http://www.w3.org">
                    <path d="M12 3L1 9l11 6 9-4.91V17h2V9M5 13.18v4L12 21l7-3.82v-4L12 17l-7-3.82z""")/>>
                </svg>
            </div>
            <h1>Academic <span class="accent-text">Pro</span></h1>
            <p>Precise GPA & CGPA Analysis</p>
        </header>

        <!-- Dynamic Scale Selection -->
        <section class="scale-box">
            <p><strong>Set 4.0 GPA</strong></p>
            <div class="scale-options">
                <input type="radio" name="threshold" id="t80" value="80">
                <label for="t80">80%</label>
                
                <input type="radio" name="threshold" id="t85" value="85" checked>
                <label for="t85">85%</label>
                
                <input type="radio" name="threshold" id="t90" value="90">
                <label for="t90">90%</label>
            </div>
        </section>

        <!-- Navigation Tabs -->
        <nav class="nav-tabs">
            <button id="gpaTabBtn" class="tab-btn active" onclick="switchTab('gpa')">Semester GPA</button>
            <button id="cgpaTabBtn" class="tab-btn" onclick="switchTab('cgpa')">Total CGPA</button>
        </nav>

        <!-- GPA Calculator Section -->
        <section id="gpa-section" class="calc-area">
            <div id="gpa-rows-container">
                <div class="input-group">
                    <input type="number" placeholder="Marks(0-100)" class="gpa-marks">
                    <input type="number" placeholder="Credits" class="gpa-credits">
                </div>
            </div>
            <button class="btn-add" onclick="addRow('gpa-rows-container')">+ Add Subject</button>
            <button class="btn-main" onclick="calculateGPA()">Calculate GPA</button>
        </section>

        <!-- CGPA Calculator Section -->
        <section id="cgpa-section" class="calc-area" style="display:none;">
            <div id="cgpa-rows-container">
                <div class="input-group">
                    <input type="number" step="0.01" placeholder="Sem GPA" class="cgpa-val">
                    <input type="number" placeholder="Sem Credits" class="cgpa-credits">
                </div>
            </div>
            <button class="btn-add" onclick="addRow('cgpa-rows-container')">+ Add Semester</button>
            <button class="btn-main" onclick="calculateCGPA()">Calculate CGPA</button>
        </section>

        <!-- Personality Result Card -->
         
        <div id="result-card" class="result-card">
            <h2 id="final-result">0.00</h2>
            <p id="congrats-msg">Your result will show here!</p>
        </div>

        <!-- SEO Details Section -->
        <article class="seo-details">
            <h3>Why use this GPA Calculator?</h3>
            <p>Our tool is designed for accuracy. By selecting a dynamic scale (80, 85, or 90), the system automatically adjusts the grade point relative to your city's academic standards. This ensures students get the most realistic representation of their academic standing.</p>
        </article>
    </main>
  


    <!-- Stylish Footer -->
    <footer class="footer">
        <div class="footer-inner">
            <p>Expertly Developed by</p>
            <h2 class="dev-name">Hammad Developer</h2>
            <div class="badges">
                <span>Fast</span> • <span>SEO Ready</span> • <span>Responsive</span>
            </div>
            <p class="copyright">© 2026 All Rights Reserved</p>
        </div>
    </footer>

    <script src="script.js"></script>
</body>
</html>


function switchTab(mode) {
    document.getElementById('gpa-section').style.display = mode === 'gpa' ? 'block' : 'none';
    document.getElementById('cgpa-section').style.display = mode === 'cgpa' ? 'block' : 'none';
    document.getElementById('gpaTabBtn').classList.toggle('active', mode === 'gpa');
    document.getElementById('cgpaTabBtn').classList.toggle('active', mode === 'cgpa');
    document.getElementById('result-card').style.display = 'none';
}

function addRow(containerId) {
    const container = document.getElementById(containerId);
    const div = document.createElement('div');
    div.className = 'input-group';
    if(containerId === 'gpa-rows-container') {
        div.innerHTML = `<input type="number" placeholder="Marks(0-100)" class="gpa-marks"><input type="number" placeholder="Credits" class="gpa-credits">`;
    } else {
        div.innerHTML = `<input type="number" step="0.01" placeholder="Sem GPA" class="cgpa-val"><input type="number" placeholder="Sem Credits" class="cgpa-credits">`;
    }
    container.appendChild(div);
}

// RELATIVE GPA CALCULATION
function getRelativePoints(marks, threshold) {
    marks = parseFloat(marks);
    const scale = parseInt(threshold);
    
    if (marks >= scale) return 4.00;
    
    // Relative shift: Every 5 marks below threshold is roughly 0.5 points
    let points = 4.0 - ((scale - marks) * 0.1);
    return points > 0 ? points.toFixed(2) : 0.00;
}

function calculateGPA() {
    const marks = document.querySelectorAll('.gpa-marks');
    const credits = document.querySelectorAll('.gpa-credits');
    const threshold = document.querySelector('input[name="threshold"]:checked').value;
    
    let totalPoints = 0, totalCredits = 0;

    marks.forEach((m, i) => {
        let mv = parseFloat(m.value);
        let cv = parseFloat(credits[i].value);
        if(!isNaN(mv) && !isNaN(cv)) {
            totalPoints += getRelativePoints(mv, threshold) * cv;
            totalCredits += cv;
        }
    });

    showFinalResult(totalCredits > 0 ? (totalPoints / totalCredits).toFixed(2) : "0.00");
}

function calculateCGPA() {
    const gpas = document.querySelectorAll('.cgpa-val');
    const credits = document.querySelectorAll('.cgpa-credits');
    
    let totalPoints = 0, totalCredits = 0;

    gpas.forEach((g, i) => {
        let gv = parseFloat(g.value);
        let cv = parseFloat(credits[i].value);
        if(!isNaN(gv) && !isNaN(cv)) {
            totalPoints += gv * cv;
            totalCredits += cv;
        }
    });

    showFinalResult(totalCredits > 0 ? (totalPoints / totalCredits).toFixed(2) : "0.00");
}

function showFinalResult(score) {
    const card = document.getElementById('result-card');
    const scoreEl = document.getElementById('final-result');
    const msgEl = document.getElementById('congrats-msg');
    
    card.style.display = 'block';
    scoreEl.innerText = score;
    
    if (parseFloat(score) >= 3.5) {
        msgEl.innerHTML = `<span style="color:#10b981">🎉 Congratulations! Good Job! 🌟</span>`;
        card.style.borderColor = "#10b981";
    } else {
        msgEl.innerHTML = "Keep striving for excellence!";
        card.style.borderColor = "#e2e8f0";
    }
    card.scrollIntoView({ behavior: 'smooth' });
}
function returnToStart() {
    // 1. Hide the result popup
    closeResult();

    // 2. Clear all input fields
    const inputs = document.querySelectorAll('input');
    inputs.forEach(input => input.value = '');

    // 3. Remove extra rows (optional: keeps only the first row)
    const subjectList = document.getElementById('subject-list');
    while (subjectList.children.length > 1) {
        subjectList.removeChild(subjectList.lastChild);
    }

    const semesterList = document.getElementById('semester-list');
    while (semesterList.children.length > 1) {
        semesterList.removeChild(semesterList.lastChild);
    }
    
    // 4. Reset result text on the main page
    document.getElementById('gpa-result').innerText = "Result: --";
    document.getElementById('cgpa-result').innerText = "Result: --";
}
function autoReset() {
    // 1. Hide the result popup
    document.getElementById('overlay').style.display = 'none';

    // 2. Clear all input fields
    document.querySelectorAll('input').forEach(input => input.value = '');

    // 3. Remove dynamically added rows (keep only the first row)
    const gpaList = document.getElementById('gpa-list');
    while (gpaList.children.length > 1) {
        gpaList.removeChild(gpaList.lastChild);
    }
}

/* =========================================
   1. ROOT VARIABLES & GLOBAL STYLES
   ========================================= */
:root {
    --primary: #6366f1;       /* Indigo */
    --primary-hover: #4f46e5;
    --success: #10b981;       /* Emerald Green */
    --dark: #0f172a;          /* Deep Navy */
    --text-main: #1e293b;
    --bg-gradient: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%);
    --glass-bg: rgba(255, 255, 255, 0.9);
}

* {
    box-sizing: border-box;
}

body {
    background-image: url(\h.jpg);
    margin: 0;
    font-family: 'Outfit', sans-serif;
    background: var(--bg-gradient);
    color: var(--text-main);
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}
/* =========================================
   2. MAIN LAYOUT (GLASS CONTAINER)
   ========================================= */
.app-wrapper {
    max-width: 500px;
    width: 92%;
    margin: 40px auto;
    background: var(--glass-bg);
    backdrop-filter: blur(12px);
    padding: 30px;
    border-radius: 30px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.08);
    border: 1px solid rgba(255, 255, 255, 0.5);
    flex-grow: 1;
}

/* =========================================
   3. HEADER & LOGO
   ========================================= */
.header {
    text-align: center;
    margin-bottom: 25px;
}

.main-svg-logo {
    width: 55px;
    fill: var(--primary);
    margin-bottom: 10px;
    transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.main-svg-logo:hover {
    transform: scale(1.15) rotate(-8deg);
}

.accent-text {
    color: var(--primary);
    font-weight: 800;
}

/* =========================================
   4. DYNAMIC SCALE BOX (80, 85, 90)
   ========================================= */
.scale-box {
    background: #eaeef3;
    padding: 15px;
    border-radius: 18px;
    text-align: center;
    margin-bottom: 20px;
    border: 1px solid #e2e8f0;
}

.scale-options {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 10px;
    font-weight: 600;
}

.scale-options label {
    cursor: pointer;
    padding: 5px 10px;
    border-radius: 8px;
    transition: background 0.3s;
}

/* =========================================
   5. NAVIGATION TABS
   ========================================= */
.nav-tabs {
    display: flex;
    background: #f1f5f9;
    padding: 6px;
    border-radius: 14px;
    margin-bottom: 20px;
}

.tab-btn {
    flex: 1;
    padding: 12px;
    border: none;
    background: transparent;
    cursor: pointer;
    font-weight: 700;
    border-radius: 10px;
    transition: 0.3s all ease;
    color: #64748b;
}

.tab-btn.active {
    background: white;
    color: var(--primary);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

/* =========================================
   6. INPUTS & ROWS
   ========================================= */
.input-group {
    display: flex;
    gap: 12px;
    margin-bottom: 12px;
    animation: slideIn 0.4s ease-out;
}

input {
    width: 100%;
    padding: 14px;
    border: 2px solid #e2e8f0;
    border-radius: 12px;
    font-size: 1rem;
    outline: none;
    transition: border-color 0.3s;
}

input:focus {
    border-color: var(--primary);
}

/* =========================================
   7. BUTTONS
   ========================================= */
.btn-add {
    width: 100%;
    padding: 12px;
    background: #f8fafc;
    border: 2px dashed #cbd5e1;
    color: var(--primary);
    border-radius: 12px;
    cursor: pointer;
    font-weight: 700;
    margin-top: 5px;
    transition: 0.3s;
}

.btn-add:hover {
    background: #eff6ff;
    border-color: var(--primary);
}

.btn-main {
    width: 100%;
    padding: 18px;
    background: var(--primary);
    color: white;
    border: none;
    border-radius: 15px;
    font-size: 1.1rem;
    font-weight: 700;
    margin-top: 25px;
    cursor: pointer;
    transition: 0.4s;
}

.btn-main:hover {
    background: var(--primary-hover);
    transform: translateY(-3px);
    box-shadow: 0 10px 20px rgba(99, 102, 241, 0.3);
}

/* =========================================
   8. RESULT CARD & PERSONALITY
   ========================================= */
.result-card {
    margin-top: 35px;
    padding: 30px;
    border-radius: 24px;
    text-align: center;
    display: none; /* Hidden until calculated */
    background: white;
    border: 3px solid #e2e8f0;
    animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

#final-result {
    font-size: 4rem;
    margin: 0;
    color: var(--primary);
    font-weight: 800;
}

#congrats-msg {
    font-size: 1.1rem;
    font-weight: 600;
    margin-top: 10px;
}

/* =========================================
   9. SEO CONTENT & FOOTER
   ========================================= */
.seo-details {
    margin-top: 50px;
    font-size: 0.9rem;
    line-height: 1.7;
    opacity: 0.7;
    border-top: 1px solid #e2e8f0;
    padding-top: 25px;
}
.reset-btn {
    background: #6c757d; /* Grey color for reset */
    color: white;
    border: none;
    padding: 12px;
    border-radius: 10px;
    width: 100%;
    margin-top: 10px;
    font-size: 16px;
    cursor: pointer;
}

/* Ensure the result box looks good on Android */
.result-box {
    display: flex;
    flex-direction: column;
    gap: 10px;
}


.footer {
    background: var(--dark);
    color: white;
    padding: 60px 20px;
    text-align: center;
    border-radius: 50px 50px 0 0;
    margin-top: 40px;
}

.dev-name {
    color: var(--success);
    margin: 10px 0;
    font-size: 2rem;
    letter-spacing: 1px;
}

.badges {
    font-size: 0.85rem;
    margin: 15px 0;
    opacity: 0.6;
}

.copyright {
    font-size: 0.75rem;
    opacity: 0.4;
}

/* =========================================
   10. ANIMATIONS & RESPONSIVENESS
   ========================================= */
@keyframes slideIn {
    from { opacity: 0; transform: translateY(15px); }
    to { opacity: 1; transform: translateY(0); }
}

@keyframes popIn {
    from { opacity: 0; transform: scale(0.9); }
    to { opacity: 1; transform: scale(1); }
}

/* Android / Mobile Phone Optimization */
@media (max-width: 480px) {
    .app-wrapper {
        padding: 20px;
        margin: 15px auto;
        border-radius: 20px;
    }
    #final-result {
        font-size: 3rem;
    }
    .scale-options {
        gap: 10px;
    }
    .footer {
        padding: 40px 15px;
    }
}
