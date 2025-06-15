<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <title>رحلة المهندس المحترف - OVO Funnel</title>
  <style>
    body {
      background-color: #111;
      color: #fff;
      font-family: 'Cairo', sans-serif;
      padding: 30px;
      max-width: 800px;
      margin: auto;
    }
    h2 {
      color: #ffba00;
      margin-bottom: 20px;
    }
    .video-box {
      margin-bottom: 40px;
    }
    iframe {
      width: 100%;
      height: 400px;
      border: none;
      border-radius: 12px;
    }
    #countdown {
      font-size: 20px;
      margin-bottom: 10px;
      text-align: center;
      color: #f00;
    }
    .debug {
      background: #222;
      padding: 10px;
      margin: 30px 0;
      border-radius: 8px;
    }
    .debug select, .debug button {
      padding: 8px 12px;
      margin-right: 10px;
      border: none;
      border-radius: 6px;
    }
  </style>
</head>
<body>

  <h1>🎓 دورة رحلة المهندس المحترف - OVO Funnel</h1>

  <!-- ✅ وضع الاختبار -->
  <div class="debug">
    <label>🧪 اختبار يوم:</label>
    <select id="daySelector">
      <option value="1">اليوم الأول</option>
      <option value="2">اليوم الثاني</option>
      <option value="3">اليوم الثالث</option>
      <option value="4">اليوم الرابع (عرض)</option>
    </select>
    <button onclick="setTestDay()">تفعيل الاختبار</button>
    <button onclick="resetAll()">إعادة التهيئة</button>
  </div>

  <div id="videos"></div>

  <script>
    const videosData = [
      { day: 1, title: "📘 فيديو اليوم الأول", url: "https://www.youtube.com/embed/VIDEO_ID_1" },
      { day: 2, title: "📗 فيديو اليوم الثاني", url: "https://www.youtube.com/embed/VIDEO_ID_2" },
      { day: 3, title: "📙 فيديو اليوم الثالث", url: "https://www.youtube.com/embed/VIDEO_ID_3" },
      { day: 4, title: "🎯 فيديو العرض", url: "https://www.youtube.com/embed/OFFER_VIDEO_ID" },
    ];

    let currentDay = 1;
    const debugDay = localStorage.getItem("debugDay");
    const storedStart = localStorage.getItem("ovoStartDate");

    if (debugDay) {
      currentDay = parseInt(debugDay);
    } else if (storedStart) {
      const startDate = new Date(storedStart);
      const now = new Date();
      const diff = Math.floor((now - startDate) / (1000 * 60 * 60 * 24)) + 1;
      currentDay = Math.min(diff, 4);
    } else {
      const today = new Date();
      localStorage.setItem("ovoStartDate", today.toISOString());
      currentDay = 1;
    }

    const container = document.getElementById("videos");
    const selectedVideo = videosData.find(v => v.day === currentDay);

    if (selectedVideo) {
      const section = document.createElement("div");
      section.className = "video-box";

      if (selectedVideo.day === 4) {
        let offerStart = localStorage.getItem("offerStartTime");

        if (!offerStart) {
          offerStart = new Date().toISOString();
          localStorage.setItem("offerStartTime", offerStart);
        }

        const countdown = document.createElement("div");
        countdown.id = "countdown";
        section.appendChild(countdown);

        updateCountdown(new Date(offerStart));
        setInterval(() => updateCountdown(new Date(offerStart)), 1000);
      }

      section.innerHTML += `
        <h2>${selectedVideo.title}</h2>
        <iframe src="${selectedVideo.url}" allowfullscreen></iframe>
      `;
      container.appendChild(section);
    }

    function updateCountdown(startTime) {
      const now = new Date();
      const end = new Date(startTime.getTime() + 24 * 60 * 60 * 1000);
      const diff = end - now;

      const cd = document.getElementById("countdown");
      if (diff <= 0) {
        cd.innerText = "⏰ انتهى الوقت!";
      } else {
        const hours = Math.floor(diff / (1000 * 60 * 60));
        const mins = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
        const secs = Math.floor((diff % (1000 * 60)) / 1000);
        cd.innerText = `⏳ ينتهي العرض خلال: ${hours} ساعة، ${mins} دقيقة، ${secs} ثانية`;
      }
    }

    function setTestDay() {
      const day = parseInt(document.getElementById("daySelector").value);
      localStorage.setItem("debugDay", day);

      if (day === 4) {
        localStorage.setItem("offerStartTime", new Date().toISOString());
      }

      location.reload();
    }

    function resetAll() {
      localStorage.removeItem("ovoStartDate");
      localStorage.removeItem("debugDay");
      localStorage.removeItem("offerStartTime");
      alert("✅ تم إعادة ضبط البيانات.");
      location.reload();
    }
  </script>

</body>
</html>
