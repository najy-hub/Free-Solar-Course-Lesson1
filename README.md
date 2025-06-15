<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>سلسلة الفيديوهات - OVO</title>
  <style>
    body {
      background-color: #111;
      color: #fff;
      font-family: 'Cairo', sans-serif;
      padding: 20px;
      max-width: 800px;
      margin: auto;
    }
    h1, h2 {
      text-align: center;
      margin-bottom: 20px;
    }
    .video-box {
      margin-bottom: 40px;
    }
    iframe {
      width: 100%;
      height: 400px;
      border-radius: 12px;
      border: none;
    }
    .timer {
      text-align: center;
      font-size: 20px;
      margin-bottom: 10px;
      color: #ffba00;
    }
    .test-controls {
      background-color: #1a1a1a;
      padding: 20px;
      border-radius: 12px;
      margin-bottom: 30px;
    }
    .test-controls select, .test-controls button {
      padding: 10px;
      font-size: 16px;
      border-radius: 6px;
      margin-left: 10px;
    }
  </style>
</head>
<body>

  <h1>🎓 سلسلة الفيديوهات التعليمية</h1>

  <div class="test-controls">
    <label>🧪 وضع الاختبار:</label>
    <select id="testDay">
      <option value="0">اختر اليوم</option>
      <option value="1">اليوم الأول</option>
      <option value="2">اليوم الثاني</option>
      <option value="3">اليوم الثالث</option>
      <option value="4">اليوم الرابع (العرض)</option>
    </select>
    <button onclick="activateTestMode()">تفعيل الاختبار</button>
    <button onclick="disableTestMode()">إلغاء</button>
  </div>

  <div id="videosContainer"></div>

  <script>
    const videos = [
      { day: 1, title: "📘 الفيديو الأول", url: "https://www.youtube.com/embed/YOUR_VIDEO_1" },
      { day: 2, title: "📗 الفيديو الثاني", url: "https://www.youtube.com/embed/YOUR_VIDEO_2" },
      { day: 3, title: "📙 الفيديو الثالث", url: "https://www.youtube.com/embed/YOUR_VIDEO_3" },
      { day: 4, title: "🎯 فيديو العرض", url: "https://www.youtube.com/embed/YOUR_OFFER_VIDEO" }
    ];

    let testMode = false;
    let testDay = 0;

    function getUserDay() {
      const start = localStorage.getItem("ovoStartDate");
      if (!start) {
        const today = new Date();
        localStorage.setItem("ovoStartDate", today.toISOString());
        return 1;
      }
      const startDate = new Date(start);
      const diff = Math.floor((new Date() - startDate) / (1000 * 60 * 60 * 24));
      return Math.min(diff + 1, 4);
    }

    function activateTestMode() {
      testDay = parseInt(document.getElementById("testDay").value);
      if (testDay > 0 && testDay <= 4) {
        testMode = true;
        renderVideos();
      }
    }

    function disableTestMode() {
      testMode = false;
      testDay = 0;
      renderVideos();
    }

    function renderVideos() {
      const container = document.getElementById("videosContainer");
      container.innerHTML = "";

      const currentDay = testMode ? testDay : getUserDay();
      const availableDays = testMode ? [currentDay] : Array.from({ length: currentDay }, (_, i) => i + 1);

      videos.forEach(video => {
        if (!availableDays.includes(video.day)) return;

        const box = document.createElement("div");
        box.className = "video-box";

        if (video.day === 4) {
          // عرض العد التنازلي
          const timer = document.createElement("div");
          timer.className = "timer";
          timer.id = "offerTimer";
          box.appendChild(timer);
          startOfferTimer();
        }

        box.innerHTML += `<h2>${video.title}</h2><iframe src="${video.url}" allowfullscreen></iframe>`;
        container.appendChild(box);
      });
    }

    function startOfferTimer() {
      const offerKey = "offerVideoStart";
      let offerStart = localStorage.getItem(offerKey);
      if (!offerStart) {
        offerStart = new Date().toISOString();
        localStorage.setItem(offerKey, offerStart);
      }

      function updateCountdown() {
        const now = new Date();
        const start = new Date(offerStart);
        const end = new Date(start.getTime() + 24 * 60 * 60 * 1000);
        const diff = end - now;

        if (diff <= 0) {
          document.getElementById("offerTimer").innerText = "⏰ انتهى الوقت!";
          return;
        }

        const hours = String(Math.floor(diff / (1000 * 60 * 60))).padStart(2, "0");
        const minutes = String(Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, "0");
        const seconds = String(Math.floor((diff % (1000 * 60)) / 1000)).padStart(2, "0");

        document.getElementById("offerTimer").innerText = `⌛ ينتهي خلال: ${hours}:${minutes}:${seconds}`;
        setTimeout(updateCountdown, 1000);
      }

      updateCountdown();
    }

    // تشغيل عند التحميل
    renderVideos();
  </script>

</body>
</html>
