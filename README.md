<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>FitHome Pro - At-Home Workouts</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');
  body {
    margin: 0; font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #000428, #004e92);
    color: #eee;
    min-height: 100vh;
    display: flex; flex-direction: column;
  }
  header {
    padding: 1.5rem 1rem;
    text-align: center;
    background: rgba(0,0,0,0.7);
    box-shadow: 0 0 20px #39f;
  }
  header h1 {
    margin: 0; font-weight: 700; font-size: 2.5rem; color: #39f;
    text-shadow: 0 0 10px #0af;
  }
  nav {
    display: flex; justify-content: center;
    background: rgba(0,0,0,0.75);
    box-shadow: inset 0 -2px 6px #39f;
  }
  nav button {
    flex: 1;
    padding: 1rem 0;
    font-size: 1.1rem;
    font-weight: 600;
    border: none;
    background: transparent;
    color: #99caff;
    cursor: pointer;
    transition: background 0.3s, color 0.3s;
  }
  nav button:hover, nav button.active {
    background: #1e90ff;
    color: white;
    box-shadow: 0 0 12px #39f;
  }
  main {
    max-width: 900px;
    margin: 2rem auto;
    padding: 0 1rem 3rem;
    flex-grow: 1;
  }
  .workout-item {
    background: rgba(0,0,0,0.6);
    border-radius: 12px;
    box-shadow: 0 0 15px #1e90ff;
    margin-bottom: 2rem;
    padding: 1rem 1.2rem 1.5rem;
    color: #ddd;
  }
  .workout-item h2 {
    margin-top: 0;
    font-size: 1.3rem;
    color: #39f;
    text-shadow: 0 0 6px #39f;
  }
  .reps {
    font-size: 1rem;
    font-weight: 600;
    margin-bottom: 8px;
    color: #aaddff;
  }
  iframe {
    width: 100%;
    height: 315px;
    border-radius: 12px;
    box-shadow: 0 0 15px #1e90ff inset;
    margin-top: 8px;
  }
  #completeWorkout {
    display: block;
    margin: 2rem auto 0;
    padding: 1rem 3rem;
    font-size: 1.3rem;
    font-weight: 700;
    background: #1e90ff;
    border: none;
    border-radius: 30px;
    color: white;
    cursor: pointer;
    box-shadow: 0 0 15px #39f;
    transition: background 0.3s ease;
  }
  #completeWorkout:disabled {
    background: #555;
    cursor: default;
    box-shadow: none;
  }
  #completeWorkout:hover:not(:disabled) {
    background: #3399ff;
  }
  #profileSection {
    display: none;
    max-width: 700px;
    margin: 0 auto;
    padding: 1rem 1rem 2rem;
    background: rgba(0,0,0,0.6);
    border-radius: 12px;
    box-shadow: 0 0 20px #1e90ff;
    color: #eee;
  }
  #profileSection h2 {
    text-align: center;
    margin-top: 0;
    font-size: 2rem;
    color: #1e90ff;
    text-shadow: 0 0 10px #39f;
  }
  .profile-info {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    margin: 1rem 0 2rem;
  }
  .profile-info div {
    flex: 1 1 150px;
    margin: 0.5rem;
    background: #121a40;
    border-radius: 10px;
    padding: 1rem;
    box-shadow: 0 0 12px #1e90ff inset;
    text-align: center;
  }
  .profile-info div span {
    display: block;
    margin-top: 0.4rem;
    font-size: 1.4rem;
    font-weight: 700;
    color: #39f;
    text-shadow: 0 0 5px #39f;
  }
  #goalInputSection {
    text-align: center;
    margin-bottom: 2rem;
  }
  #goalInputSection input[type="number"] {
    padding: 0.5rem 0.7rem;
    font-size: 1.1rem;
    width: 80px;
    border-radius: 6px;
    border: 1px solid #39f;
    background: #001022;
    color: #eee;
    text-align: center;
    outline: none;
  }
  #goalInputSection button {
    margin-left: 10px;
    padding: 0.5rem 1rem;
    font-size: 1.1rem;
    font-weight: 700;
    background: #1e90ff;
    border: none;
    border-radius: 8px;
    color: white;
    cursor: pointer;
    box-shadow: 0 0 10px #39f;
    transition: background 0.3s ease;
  }
  #goalInputSection button:hover {
    background: #3399ff;
  }
  .progress-bar {
    width: 100%;
    background: #222;
    height: 24px;
    border-radius: 30px;
    box-shadow: inset 0 0 8px #0a3eff;
    overflow: hidden;
  }
  .progress-bar-inner {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, #0a7fff, #00d4ff);
    border-radius: 30px;
    box-shadow: 0 0 10px #1e90ff;
    transition: width 1.2s ease;
  }
  #avatarContainer {
    display: flex;
    justify-content: center;
    gap: 20px;
    flex-wrap: wrap;
  }
  .avatar {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    border: 3px solid transparent;
    cursor: pointer;
    box-shadow: 0 0 8px #39f;
    transition: border-color 0.4s ease;
  }
  .avatar.selected {
    border-color: #1e90ff;
  }
  @media (max-width: 600px) {
    iframe {height: 200px;}
    nav button {font-size: 1rem;}
  }
</style>
</head>
<body>

<header><h1>FitHome Pro</h1></header>
<nav>
  <button id="btnHome" class="active" onclick="showHome()">Home</button>
  <button id="btnProfile" onclick="showProfile()">Profile</button>
</nav>

<main>
  <section id="homeSection">
    <div id="workoutList"></div>
    <button id="completeWorkout">Complete Workout</button>
  </section>

  <section id="profileSection">
    <h2>Your Profile</h2>
    <div class="profile-info">
      <div>
        <div>Level</div>
        <span id="userLevel">1</span>
      </div>
      <div>
        <div>Workouts Completed</div>
        <span id="workoutsCompletedDisplay">0</span>
      </div>
      <div>
        <div>Weight Lost (lbs)</div>
        <span id="weightLost">0.0</span>
      </div>
    </div>
    <div id="goalInputSection">
      <label for="goalWeight" style="font-weight:700;">Set Weight Loss Goal (lbs): </label>
      <input type="number" id="goalWeight" min="1" max="500" step="0.1" />
      <button onclick="saveGoals()">Save</button>
    </div>
    <div class="progress-bar" title="Progress to goal weight loss">
      <div id="weightProgressBar" class="progress-bar-inner"></div>
    </div>
    <h3 style="text-align:center; margin-top: 2rem;">Select Avatar</h3>
    <div id="avatarContainer"></div>
  </section>
</main>

<script>
  const workouts = [
    [
      {name:"100 Jumping Jacks", reps:"100 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/c4DAnQ6DtF8"},
      {name:"30 Bodyweight Squats", reps:"30 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/aclHkVaku9U"},
      {name:"20 Wall Push-ups", reps:"20 reps (approx 3 mins)", youtube:"https://www.youtube.com/embed/IODxDxX7oi4"},
      {name:"20 Lunges (each leg)", reps:"20 reps per leg (approx 6 mins)", youtube:"https://www.youtube.com/embed/QOVaHwm-Q6U"},
      {name:"45-sec Plank", reps:"45 seconds", youtube:"https://www.youtube.com/embed/pSHjTRCQxIw"},
      {name:"30-sec Superman Hold", reps:"30 seconds", youtube:"https://www.youtube.com/embed/z6PJMT2y8GQ"},
      {name:"15 Burpees", reps:"15 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/dZgVxmf6jkA"},
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"}
    ],
    [
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"},
      {name:"40-second High Knees", reps:"40 seconds", youtube:"https://www.youtube.com/embed/OAJ_J3EZkdY"},
      {name:"25 Jump Squats", reps:"25 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/0Gq3tKQffKU"},
      {name:"30-second Side Plank (each side)", reps:"30 seconds each side", youtube:"https://www.youtube.com/embed/KY5L6woc4fE"},
      {name:"30-second Glute Bridge", reps:"30 seconds", youtube:"https://www.youtube.com/embed/m2Zx-0fJ2a8"},
      {name:"15 Burpees", reps:"15 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/dZgVxmf6jkA"},
      {name:"30 Push-ups", reps:"30 reps (approx 6 mins)", youtube:"https://www.youtube.com/embed/IODxDxX7oi4"},
      {name:"40-second Wall Sit", reps:"40 seconds", youtube:"https://www.youtube.com/embed/-h1k88xG0Ug"}
    ],
    [
      {name:"60-second Jump Rope (imaginary)", reps:"60 seconds", youtube:"https://www.youtube.com/embed/M7cd_mkFNxk"},
      {name:"30 Push-ups (modified if needed)", reps:"30 reps (approx 6 mins)", youtube:"https://www.youtube.com/embed/IODxDxX7oi4"},
      {name:"40-second Wall Sit", reps:"40 seconds", youtube:"https://www.youtube.com/embed/-h1k88xG0Ug"},
      {name:"25 Glute Kickbacks", reps:"25 reps each leg (approx 5 mins)", youtube:"https://www.youtube.com/embed/8zreJXgx0-I"},
      {name:"30-second Plank Shoulder Taps", reps:"30 seconds", youtube:"https://www.youtube.com/embed/AAkCzYO4_Hs"},
      {name:"20-second Hollow Body Hold", reps:"20 seconds", youtube:"https://www.youtube.com/embed/0ZX7rg1u7kA"},
      {name:"30 Bodyweight Squats", reps:"30 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/aclHkVaku9U"},
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"}
    ],
    [
      {name:"40 Jump Lunges", reps:"40 reps (approx 7 mins)", youtube:"https://www.youtube.com/embed/1uFz5oJp8v0"},
      {name:"25-second Bear Crawl", reps:"25 seconds", youtube:"https://www.youtube.com/embed/otGkRBvy1ZI"},
      {name:"20 Incline Push-ups", reps:"20 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/sWm2hO6LSSs"},
      {name:"40-second Side Plank with Leg Lift", reps:"40 seconds each side", youtube:"https://www.youtube.com/embed/A7Y3Cm8NYKo"},
      {name:"30-second Superman Hold", reps:"30 seconds", youtube:"https://www.youtube.com/embed/z6PJMT2y8GQ"},
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"},
      {name:"15 Burpees", reps:"15 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/dZgVxmf6jkA"},
      {name:"45-sec Plank", reps:"45 seconds", youtube:"https://www.youtube.com/embed/pSHjTRCQxIw"}
    ],
    [
      {name:"30-second Jump Rope (imaginary)", reps:"30 seconds", youtube:"https://www.youtube.com/embed/M7cd_mkFNxk"},
      {name:"50 Bodyweight Squats", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/aclHkVaku9U"},
      {name:"25 Push-ups", reps:"25 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/IODxDxX7oi4"},
      {name:"40-second Wall Sit", reps:"40 seconds", youtube:"https://www.youtube.com/embed/-h1k88xG0Ug"},
      {name:"40-second Plank", reps:"40 seconds", youtube:"https://www.youtube.com/embed/pSHjTRCQxIw"},
      {name:"15 Burpees", reps:"15 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/dZgVxmf6jkA"},
      {name:"30 Lunges (each leg)", reps:"30 reps each leg (approx 7 mins)", youtube:"https://www.youtube.com/embed/QOVaHwm-Q6U"},
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"}
    ],
    [
      {name:"25 Jump Squats", reps:"25 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/0Gq3tKQffKU"},
      {name:"20 Lunges (each leg)", reps:"20 reps per leg (approx 6 mins)", youtube:"https://www.youtube.com/embed/QOVaHwm-Q6U"},
      {name:"30-second Glute Bridge", reps:"30 seconds", youtube:"https://www.youtube.com/embed/m2Zx-0fJ2a8"},
      {name:"20 Wall Push-ups", reps:"20 reps (approx 3 mins)", youtube:"https://www.youtube.com/embed/IODxDxX7oi4"},
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"},
      {name:"45-sec Plank", reps:"45 seconds", youtube:"https://www.youtube.com/embed/pSHjTRCQxIw"},
      {name:"30-second Superman Hold", reps:"30 seconds", youtube:"https://www.youtube.com/embed/z6PJMT2y8GQ"},
      {name:"15 Burpees", reps:"15 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/dZgVxmf6jkA"}
    ],
    [
      {name:"15 Burpees", reps:"15 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/dZgVxmf6jkA"},
      {name:"40-second Side Plank (each side)", reps:"40 seconds each", youtube:"https://www.youtube.com/embed/KY5L6woc4fE"},
      {name:"30 Push-ups", reps:"30 reps (approx 6 mins)", youtube:"https://www.youtube.com/embed/IODxDxX7oi4"},
      {name:"30 Bodyweight Squats", reps:"30 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/aclHkVaku9U"},
      {name:"30-second Superman Hold", reps:"30 seconds", youtube:"https://www.youtube.com/embed/z6PJMT2y8GQ"},
      {name:"100 Jumping Jacks", reps:"100 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/c4DAnQ6DtF8"},
      {name:"50 Mountain Climbers", reps:"50 reps (approx 5 mins)", youtube:"https://www.youtube.com/embed/nmwgirgXLYM"},
      {name:"30-second Plank Shoulder Taps", reps:"30 seconds", youtube:"https://www.youtube.com/embed/AAkCzYO4_Hs"}
    ],
  ];

  // avatars: you can replace these URLs with your own images or local paths
  const avatars = [
    "https://i.pravatar.cc/80?img=1",
    "https://i.pravatar.cc/80?img=5",
    "https://i.pravatar.cc/80?img=10",
    "https://i.pravatar.cc/80?img=12",
    "https://i.pravatar.cc/80?img=13",
  ];

  let userData = {
    level: 1,
    workoutsCompleted: 0,
    weightLost: 0,
    avatarIndex: 0,
    goalWeightLoss: 10,
    lastWorkoutDate: null
  };

  // Utility: format date yyyy-mm-dd
  function formatDate(date) {
    return date.toISOString().split('T')[0];
  }

  // Load user data from localStorage or init
  function loadUserData() {
    const saved = localStorage.getItem("fitHomeUserData");
    if (saved) {
      userData = JSON.parse(saved);
    } else {
      saveUserData();
    }
  }
  function saveUserData() {
    localStorage.setItem("fitHomeUserData", JSON.stringify(userData));
  }

  // Calculate current day index (0-6) from today
  function getTodayIndex() {
    const startDate = new Date("2025-07-01"); // fixed start date
    const today = new Date();
    const diffDays = Math.floor((today - startDate) / (1000*60*60*24));
    return diffDays % workouts.length;
  }

  // Render today's workouts
  function renderWorkouts() {
    const container = document.getElementById("workoutList");
    container.innerHTML = "";
    const todayIndex = getTodayIndex();
    const todayWorkouts = workouts[todayIndex];

    todayWorkouts.forEach((w, i) => {
      const div = document.createElement("div");
      div.className = "workout-item";

      const title = document.createElement("h2");
      title.textContent = w.name;
      div.appendChild(title);

      const reps = document.createElement("div");
      reps.className = "reps";
      reps.textContent = w.reps;
      div.appendChild(reps);

      const iframe = document.createElement("iframe");
      iframe.src = w.youtube + "?rel=0&autoplay=0&controls=1";
      iframe.allow = "accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture";
      iframe.allowFullscreen = true;
      div.appendChild(iframe);

      container.appendChild(div);
    });

    // Disable Complete button if already done today
    const completeBtn = document.getElementById("completeWorkout");
    const todayStr = formatDate(new Date());
    if (userData.lastWorkoutDate === todayStr) {
      completeBtn.disabled = true;
      completeBtn.textContent = "Workout Completed Today ✓";
    } else {
      completeBtn.disabled = false;
      completeBtn.textContent = "Complete Workout";
    }
  }

  // When user clicks Complete Workout
  function completeWorkout() {
    const todayStr = formatDate(new Date());
    if (userData.lastWorkoutDate !== todayStr) {
      userData.workoutsCompleted++;
      userData.lastWorkoutDate = todayStr;

      // Increase level every 5 workouts
      if (userData.workoutsCompleted % 5 === 0) {
        userData.level++;
        userData.weightLost += 0.5; // example weight loss increment per level
      }
      saveUserData();
      renderWorkouts();
      renderProfile();
      alert("Great job! Workout marked complete for today.");
    }
  }

  // Render profile info
  function renderProfile() {
    document.getElementById("userLevel").textContent = userData.level;
    document.getElementById("workoutsCompletedDisplay").textContent = userData.workoutsCompleted;
    document.getElementById("weightLost").textContent = userData.weightLost.toFixed(1);

    // Progress bar update
    const goal = userData.goalWeightLoss;
    const progress = Math.min(userData.weightLost / goal * 100, 100);
    document.getElementById("weightProgressBar").style.width = progress + "%";

    // Avatar highlight
    const avatarImgs = document.querySelectorAll(".avatar");
    avatarImgs.forEach((img, idx) => {
      img.classList.toggle("selected", idx === userData.avatarIndex);
    });
  }

  // Save goal weight loss from input
  function saveGoals() {
    const goalInput = document.getElementById("goalWeight");
    let val = parseFloat(goalInput.value);
    if (!isNaN(val) && val > 0) {
      userData.goalWeightLoss = val;
      saveUserData();
      renderProfile();
      alert("Goal saved!");
    } else {
      alert("Please enter a valid weight loss goal.");
    }
  }

  // Show avatars and handle selection
  function renderAvatars() {
    const container = document.getElementById("avatarContainer");
    container.innerHTML = "";
    avatars.forEach((url, idx) => {
      const img = document.createElement("img");
      img.src = url;
      img.alt = "Avatar " + (idx + 1);
      img.className = "avatar" + (idx === userData.avatarIndex ? " selected" : "");
      img.addEventListener("click", () => {
        userData.avatarIndex = idx;
        saveUserData();
        renderProfile();
      });
      container.appendChild(img);
    });
  }

  // Show Home or Profile sections
  function showHome() {
    document.getElementById("homeSection").style.display = "block";
    document.getElementById("profileSection").style.display = "none";
    document.getElementById("btnHome").classList.add("active");
    document.getElementById("btnProfile").classList.remove("active");
  }
  function showProfile() {
    document.getElementById("homeSection").style.display = "none";
    document.getElementById("profileSection").style.display = "block";
    document.getElementById("btnHome").classList.remove("active");
    document.getElementById("btnProfile").classList.add("active");
  }

  // Initial setup
  function init() {
    loadUserData();
    renderWorkouts();
    renderProfile();
    renderAvatars();

    document.getElementById("completeWorkout").onclick = completeWorkout;
    document.getElementById("goalWeight").value = userData.goalWeightLoss;

    showHome();
  }

  window.onload = init;
</script>

</body>
</html>
