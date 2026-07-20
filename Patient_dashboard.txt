/*==================================================
            Medicare+
        Patient Dashboard
            JS PART 1
==================================================*/


document.addEventListener("DOMContentLoaded", () => {

    /*==============================
            WELCOME NAME
    ==============================*/

    const patientName = localStorage.getItem("patientName") || "John Doe";

    document.getElementById("patientName").textContent = patientName;



    /*==============================
            DARK MODE
    ==============================*/

    const themeBtn = document.getElementById("themeToggle");

    if(themeBtn){

        themeBtn.addEventListener("click",()=>{

            document.body.classList.toggle("dark");

            const icon = themeBtn.querySelector("i");

            if(document.body.classList.contains("dark")){

                icon.classList.remove("fa-moon");

                icon.classList.add("fa-sun");

            }

            else{

                icon.classList.remove("fa-sun");

                icon.classList.add("fa-moon");

            }

        });

    }



    /*==============================
        SIDEBAR ACTIVE MENU
    ==============================*/

    const menuItems = document.querySelectorAll(".menu li");

    menuItems.forEach(item=>{

        item.addEventListener("click",()=>{

            menuItems.forEach(i=>i.classList.remove("active"));

            item.classList.add("active");

        });

    });



    /*==============================
            LOGOUT
    ==============================*/

    const logoutBtn = document.getElementById("logoutBtn");

    if(logoutBtn){

        logoutBtn.addEventListener("click",()=>{

            const confirmLogout = confirm("Do you really want to logout?");

            if(confirmLogout){

                window.location.href="patient-login.html";

            }

        });

    }



    /*==============================
        NOTIFICATION BUTTON
    ==============================*/

    const bell = document.querySelector(".icon-btn");

    if(bell){

        bell.addEventListener("click",()=>{

            alert("🔔 No new notifications.");

        });

    }



    /*==============================
            SEARCH
    ==============================*/

    const searchInput = document.querySelector(".search-box input");

    if(searchInput){

        searchInput.addEventListener("keyup",(e)=>{

            console.log("Searching:",e.target.value);

        });

    }



    /*==============================
            LIVE DATE
    ==============================*/

    function updateTime(){

        const now = new Date();

        console.log(now.toLocaleString());

    }

    updateTime();

    setInterval(updateTime,1000);

});
/*==================================================
        Medicare+
        Patient Dashboard
        JS PART 2
==================================================*/


/*==============================
        HEALTH CHART
==============================*/

const chartCanvas = document.getElementById("healthChart");

if(chartCanvas){

    new Chart(chartCanvas,{

        type:"line",

        data:{

            labels:[
                "Mon",
                "Tue",
                "Wed",
                "Thu",
                "Fri",
                "Sat",
                "Sun"
            ],

            datasets:[{

                label:"Health Score",

                data:[
                    82,
                    85,
                    87,
                    90,
                    91,
                    92,
                    94
                ],

                borderColor:"#2563eb",

                backgroundColor:"rgba(37,99,235,.15)",

                borderWidth:3,

                fill:true,

                tension:.4,

                pointRadius:5,

                pointHoverRadius:8

            }]

        },

        options:{

    responsive:true,

    maintainAspectRatio:true,

    aspectRatio:2.8,

    plugins:{

        legend:{

            display:false

        }

    },

    scales:{

        y:{

            beginAtZero:false,

            min:70,

            max:100

        }

    }

}

    });

}



/*==============================
        WATER INTAKE
==============================*/

let glasses = 6;

const waterCircle = document.querySelector(".progress-circle h2");

if(waterCircle){

    waterCircle.innerHTML = `${glasses}/8`;

}



/*==============================
    HEALTH SCORE ANIMATION
==============================*/

const healthValue = document.querySelector(".health-card h2");

if(healthValue){

    let score = 0;

    const target = 92;

    const counter = setInterval(()=>{

        score++;

        healthValue.innerHTML = score + "%";

        if(score >= target){

            clearInterval(counter);

        }

    },20);

}



/*==============================
    MEDICINE REMINDER
==============================*/

setTimeout(()=>{

    alert("💊 Reminder: Take your Morning Medicine.");

},5000);



/*==============================
    APPOINTMENT REMINDER
==============================*/

setTimeout(()=>{

    alert("📅 You have an appointment today at 4:30 PM.");

},9000);



/*==============================
        CARD ANIMATION
==============================*/

const cards = document.querySelectorAll(".card");

cards.forEach((card,index)=>{

    card.style.opacity="0";

    card.style.transform="translateY(40px)";

    setTimeout(()=>{

        card.style.transition=".6s";

        card.style.opacity="1";

        card.style.transform="translateY(0)";

    },index*200);

});



/*==============================
        QUICK ACTIONS
==============================*/

const actionButtons=document.querySelectorAll(".quick-actions button");

actionButtons.forEach(button=>{

    button.addEventListener("click",()=>{

        alert(button.innerText + " feature will be connected with backend.");

    });

});
/*==================================================
        Medicare+
        Patient Dashboard
        JS PART 3
==================================================*/


/*==============================
        SAVE DARK MODE
==============================*/

const themeButton = document.getElementById("themeToggle");

if(localStorage.getItem("theme") === "dark"){

    document.body.classList.add("dark");

    if(themeButton){

        themeButton.innerHTML =
        '<i class="fa-solid fa-sun"></i>';

    }

}

if(themeButton){

    themeButton.addEventListener("click",()=>{

        if(document.body.classList.contains("dark")){

            localStorage.setItem("theme","dark");

        }

        else{

            localStorage.setItem("theme","light");

        }

    });

}



/*==============================
        TOAST MESSAGE
==============================*/

function showToast(message,color="#2563eb"){

    const toast=document.createElement("div");

    toast.innerHTML=message;

    toast.style.position="fixed";

    toast.style.top="25px";

    toast.style.right="25px";

    toast.style.padding="15px 25px";

    toast.style.background=color;

    toast.style.color="#fff";

    toast.style.borderRadius="12px";

    toast.style.boxShadow="0 10px 25px rgba(0,0,0,.2)";

    toast.style.zIndex="9999";

    toast.style.opacity="0";

    toast.style.transition=".4s";

    document.body.appendChild(toast);

    setTimeout(()=>{

        toast.style.opacity="1";

    },100);

    setTimeout(()=>{

        toast.style.opacity="0";

        setTimeout(()=>{

            toast.remove();

        },500);

    },3000);

}



/*==============================
        SEARCH
==============================*/

const search=document.querySelector(".search-box input");

if(search){

    search.addEventListener("keyup",()=>{

        const value=search.value.toLowerCase();

        console.log("Searching :",value);

    });

}



/*==============================
        CALENDAR
==============================*/

const dates=document.querySelectorAll(".calendar-grid span");

dates.forEach(date=>{

    date.addEventListener("click",()=>{

        if(date.innerText!==""){

            showToast(

                "Selected Date : "+date.innerText,

                "#2563eb"

            );

        }

    });

});



/*==============================
    EMERGENCY CALL
==============================*/

const emergency=document.querySelector(".emergency-card button");

if(emergency){

    emergency.addEventListener("click",()=>{

        showToast(

            "Calling Emergency Contact...",

            "#ef4444"

        );

    });

}



/*==============================
    WATER INTAKE
==============================*/

const water=document.querySelector(".progress-circle h2");

let waterCount=6;

if(water){

    water.addEventListener("click",()=>{

        if(waterCount<8){

            waterCount++;

            water.innerHTML=waterCount+"/8";

            showToast(

                "Water Intake Updated 💧",

                "#06b6d4"

            );

        }

        else{

            showToast(

                "Daily Goal Completed 🎉",

                "#16a34a"

            );

        }

    });

}



/*==============================
    LIVE DASHBOARD UPDATE
==============================*/

setInterval(()=>{

    console.log("Dashboard Synced");

},30000);



/*==============================
    BACKEND READY
==============================*/

async function fetchPatientData(){

    /*

    const response=await fetch(

        "http://localhost:5000/api/patient/dashboard"

    );

    const data=await response.json();

    console.log(data);

    */

}



/*==============================
    INITIALIZE
==============================*/

window.addEventListener("load",()=>{

    showToast(

        "Welcome to Medicare+ Dashboard",

        "#2563eb"

    );

    fetchPatientData();

});



console.log("Patient Dashboard Ready");