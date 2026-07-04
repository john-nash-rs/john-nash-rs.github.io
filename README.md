<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Private Family Trip Decider</title>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

:root{
    --glass: rgba(255,255,255,0.12);
    --border: rgba(255,255,255,0.18);
    --text: rgba(255,255,255,0.95);
    --muted: rgba(255,255,255,0.72);
}

body{
    font-family:'Inter',sans-serif;
    min-height:100vh;
    background:
        radial-gradient(circle at top left,#4f46e5,transparent 35%),
        radial-gradient(circle at top right,#0ea5e9,transparent 35%),
        radial-gradient(circle at bottom,#ec4899,transparent 35%),
        #0f172a;
    color:var(--text);
    padding:20px;
}

.container{
    max-width:1400px;
    margin:auto;
}

.glass{
    background:var(--glass);
    border:1px solid var(--border);
    backdrop-filter: blur(24px);
    -webkit-backdrop-filter: blur(24px);
    border-radius:28px;
    box-shadow:
        0 20px 60px rgba(0,0,0,0.25),
        inset 0 1px 1px rgba(255,255,255,0.1);
}

.hero{
    text-align:center;
    margin-bottom:30px;
}

.hero h1{
    font-size:clamp(2rem,5vw,4rem);
    letter-spacing:-2px;
}

.hero p{
    margin-top:10px;
    color:var(--muted);
}

.tabs{
    position:sticky;
    top:20px;
    z-index:10;
    display:flex;
    justify-content:center;
    gap:12px;
    margin-bottom:25px;
}

.tab{
    padding:14px 22px;
    border-radius:999px;
    cursor:pointer;
    background:var(--glass);
    border:1px solid var(--border);
    transition:0.25s ease;
}

.tab.active{
    background:rgba(255,255,255,0.25);
}

.tab-content{
    display:none;
}

.tab-content.active{
    display:block;
}

.comparison{
    padding:20px;
    overflow:auto;
}

table{
    width:100%;
    border-collapse:collapse;
}

th, td{
    padding:18px;
    text-align:center;
}

th{
    color:white;
}

td{
    border-top:1px solid rgba(255,255,255,0.08);
    color:var(--muted);
}

.score{
    padding:8px 14px;
    border-radius:999px;
    font-size:13px;
    font-weight:600;
}

.high{
    background:rgba(34,197,94,0.18);
    color:#bbf7d0;
}

.medium{
    background:rgba(250,204,21,0.18);
    color:#fde68a;
}

.low{
    background:rgba(239,68,68,0.18);
    color:#fecaca;
}

.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
    gap:20px;
}

.card{
    padding:24px;
    transition:.25s ease;
}

.card:hover{
    transform:translateY(-6px);
}

.card h3{
    margin-bottom:15px;
}

.card ul{
    list-style:none;
}

.card li{
    padding:10px 0;
    border-bottom:1px solid rgba(255,255,255,0.08);
    color:var(--muted);
}

.card li:last-child{
    border-bottom:none;
}

.meta{
    margin-top:14px;
    display:flex;
    gap:8px;
    flex-wrap:wrap;
}

.pill{
    padding:8px 12px;
    border-radius:999px;
    background:rgba(255,255,255,0.08);
    font-size:12px;
    color:var(--muted);
}

#auth-screen{
    min-height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.auth-box{
    width:100%;
    max-width:420px;
    padding:30px;
    text-align:center;
}

.auth-box h2{
    margin-bottom:10px;
}

.auth-box p{
    color:var(--muted);
    margin-bottom:20px;
}

.auth-box input{
    width:100%;
    padding:14px;
    margin-bottom:12px;
    border:none;
    border-radius:14px;
    background:rgba(255,255,255,0.12);
    color:white;
    outline:none;
}

.auth-box button{
    width:100%;
    padding:14px;
    border:none;
    border-radius:14px;
    background:white;
    color:black;
    font-weight:600;
    cursor:pointer;
}

#error{
    margin-top:15px;
    color:#fecaca;
}

@media(max-width:768px){
    body{
        padding:16px;
    }

    .tabs{
        overflow-x:auto;
        justify-content:flex-start;
    }

    table{
        min-width:700px;
    }
}
</style>
</head>
<body>

<!-- AUTH SCREEN -->
<div id="auth-screen">
    <div class="auth-box glass">
        <h2>🔒 Private Trip Board</h2>
        <p>Harsh & Khayali 👶 Rudy</p>

        <input type="text" id="username" placeholder="Username">
        <input type="password" id="password" placeholder="Password">

        <button onclick="login()">Unlock</button>

        <p id="error"></p>
    </div>
</div>

<!-- MAIN APP -->
<div id="app" style="display:none;">
    <div class="container">

        <div class="hero">
            <h1>Where should we go?</h1>
            <p>Choose the best family destination ✈️</p>
        </div>

        <div class="tabs">
            <div class="tab active" onclick="switchTab(event,'compare')">Compare</div>
            <div class="tab" onclick="switchTab(event,'places')">Places</div>
        </div>

        <!-- Compare -->
        <div id="compare" class="tab-content active">
            <div class="glass comparison">
                <table>
                    <tr>
                        <th>Factor</th>
                        <th>🇦🇿 Azerbaijan</th>
                        <th>🇱🇰 Sri Lanka</th>
                        <th>🇹🇭 Phuket</th>
                        <th>🇻🇳 Vietnam</th>
                    </tr>

                    <tr>
                        <td>Toddler Friendly</td>
                        <td><span class="score medium">7/10</span></td>
                        <td><span class="score high">9/10</span></td>
                        <td><span class="score high">10/10</span></td>
                        <td><span class="score medium">6/10</span></td>
                    </tr>

                    <tr>
                        <td>Romance</td>
                        <td><span class="score medium">7/10</span></td>
                        <td><span class="score high">9/10</span></td>
                        <td><span class="score high">8/10</span></td>
                        <td><span class="score medium">7/10</span></td>
                    </tr>

                    <tr>
                        <td>Adventure</td>
                        <td><span class="score medium">7/10</span></td>
                        <td><span class="score high">8/10</span></td>
                        <td><span class="score low">5/10</span></td>
                        <td><span class="score high">10/10</span></td>
                    </tr>

                    <tr>
                        <td>Budget</td>
                        <td><span class="score high">8/10</span></td>
                        <td><span class="score high">9/10</span></td>
                        <td><span class="score medium">7/10</span></td>
                        <td><span class="score high">10/10</span></td>
                    </tr>
                </table>
            </div>
        </div>

        <!-- Places -->
        <div id="places" class="tab-content">
            <div class="grid">

                <div class="glass card">
                    <h3>🇦🇿 Azerbaijan</h3>
                    <ul>
                        <li>Baku Old City</li>
                        <li>Flame Towers</li>
                        <li>Gabala Mountains</li>
                        <li>Gobustan Volcanoes</li>
                        <li>Sheki Palace</li>
                    </ul>
                    <div class="meta">
                        <span class="pill">Luxury</span>
                        <span class="pill">Culture</span>
                    </div>
                </div>

                <div class="glass card">
                    <h3>🇱🇰 Sri Lanka</h3>
                    <ul>
                        <li>Sigiriya Rock</li>
                        <li>Ella Train Ride</li>
                        <li>Mirissa Beach</li>
                        <li>Yala Safari</li>
                        <li>Tea Gardens</li>
                    </ul>
                    <div class="meta">
                        <span class="pill">Nature</span>
                        <span class="pill">Romance</span>
                    </div>
                </div>

                <div class="glass card">
                    <h3>🇹🇭 Phuket</h3>
                    <ul>
                        <li>Patong Beach</li>
                        <li>Kata Beach</li>
                        <li>Phi Phi Islands</li>
                        <li>Big Buddha</li>
                        <li>Old Phuket Town</li>
                    </ul>
                    <div class="meta">
                        <span class="pill">Relax</span>
                        <span class="pill">Beach</span>
                    </div>
                </div>

                <div class="glass card">
                    <h3>🇻🇳 Vietnam</h3>
                    <ul>
                        <li>Hanoi Old Quarter</li>
                        <li>Ha Long Bay</li>
                        <li>Hoi An</li>
                        <li>Da Nang Beach</li>
                        <li>Bana Hills</li>
                    </ul>
                    <div class="meta">
                        <span class="pill">Food</span>
                        <span class="pill">Adventure</span>
                    </div>
                </div>

            </div>
        </div>

    </div>
</div>

<script>
const STATIC_USERNAME = "khayali";
const STATIC_PASSWORD = "rudy2026";

function login(){
    const username = document.getElementById("username").value;
    const password = document.getElementById("password").value;

    if(username === STATIC_USERNAME && password === STATIC_PASSWORD){
        document.getElementById("auth-screen").style.display = "none";
        document.getElementById("app").style.display = "block";
        localStorage.setItem("trip_auth","true");
    } else {
        document.getElementById("error").innerText = "Invalid username or password";
    }
}

window.onload = function(){
    if(localStorage.getItem("trip_auth") === "true"){
        document.getElementById("auth-screen").style.display = "none";
        document.getElementById("app").style.display = "block";
    }
};

function switchTab(event, tabId){
    document.querySelectorAll(".tab-content").forEach(el=>{
        el.classList.remove("active");
    });

    document.querySelectorAll(".tab").forEach(el=>{
        el.classList.remove("active");
    });

    document.getElementById(tabId).classList.add("active");
    event.currentTarget.classList.add("active");
}
</script>

</body>
</html>