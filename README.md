# Jordanlive
<meta name='viewport' content='width=device-width, initial-scale=1'/><!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>جدول مباريات كرة القدم - يلا شوت</title>
<style>
    body { font-family: Arial, sans-serif; background-color: #f4f4f4; margin: 0; padding: 0; }
    .container { width: 90%; max-width: 1000px; margin: 20px auto; }
    h1 { text-align: center; margin-bottom: 20px; color: #E50914; }
    /* نموذج إضافة مباراة */
    #addForm { background-color: #fff; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.2); margin-bottom: 20px; }
    #addForm input { width: 100%; padding: 8px; margin: 5px 0; box-sizing: border-box; border-radius: 5px; border: 1px solid #ccc; }
    #addForm button { padding: 10px 20px; background-color: #E50914; color: white; border: none; border-radius: 5px; cursor: pointer; }
    #addForm button:hover { background-color: #b20710; }

    /* بطاقات المباريات */
    .matches { display: flex; flex-direction: column; gap: 10px; }
    .match { background-color: #fff; padding: 15px; border-radius: 10px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 5px rgba(0,0,0,0.2); }
    .match .teams { font-weight: bold; font-size: 18px; }
    .match .date { color: #555; }
    .match a { text-decoration: none; background-color: #E50914; color: white; padding: 5px 10px; border-radius: 5px; }
    .match a:hover { background-color: #b20710; }
    .match button { background-color: red; color: white; padding: 5px 10px; border: none; border-radius: 5px; cursor: pointer; }
</style>
</head>
<body>
<div class="container">
    <h1>جدول مباريات كرة القدم - يلا شوت</h1>

    <!-- نموذج إضافة مباراة -->
    <div id="addForm">
        <h2>إضافة مباراة جديدة</h2>
        <input type="text" id="team1" placeholder="الفريق الأول">
        <input type="text" id="team2" placeholder="الفريق الثاني">
        <input type="datetime-local" id="date">
        <input type="url" id="link" placeholder="رابط البث الرسمي">
        <button onclick="addMatch()">إضافة المباراة</button>
    </div>

    <!-- حاوية المباريات -->
    <div class="matches" id="matchesContainer"></div>
</div>

<script>
    // قاعدة البيانات داخل الكود
    let matches = [
        {team1: "مانشستر يونايتد", team2: "ليفربول", date: "2025-11-10T20:00", link: "https://www.official-stream.com/match1"},
        {team1: "ريال مدريد", team2: "برشلونة", date: "2025-11-12T22:00", link: "https://www.official-stream.com/match2"}
    ];

    function renderMatches() {
        const container = document.getElementById("matchesContainer");
        container.innerHTML = "";
        matches.forEach((match, index) => {
            const div = document.createElement("div");
            div.className = "match";
            div.innerHTML = `
                <div>
                    <div class="teams">${match.team1} vs ${match.team2}</div>
                    <div class="date">${new Date(match.date).toLocaleString('ar-EG', { hour12: false })}</div>
                </div>
                <div>
                    <a href="${match.link}" target="_blank">مشاهدة البث</a>
                    <button onclick="removeMatch(${index})">حذف</button>
                </div>
            `;
            container.appendChild(div);
        });
    }

    function addMatch() {
        const team1 = document.getElementById("team1").value;
        const team2 = document.getElementById("team2").value;
        const date = document.getElementById("date").value;
        const link = document.getElementById("link").value;

        if(team1 && team2 && date && link) {
            matches.push({team1, team2, date, link});
            document.getElementById("team1").value = "";
            document.getElementById("team2").value = "";
            document.getElementById("date").value = "";
            document.getElementById("link").value = "";
            renderMatches();
        } else {
            alert("الرجاء تعبئة جميع الحقول!");
        }
    }

    function removeMatch(index) {
        matches.splice(index, 1);
        renderMatches();
    }

    // عرض المباريات عند التحميل
    renderMatches();
</script>
</body>
</html>
