<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>دورة الطاقة الشمسية - OVO</title>
  <style>
    body {
      background: #111;
      color: #fff;
      font-family: 'Cairo', sans-serif;
      padding: 40px 20px;
      max-width: 800px;
      margin: auto;
      line-height: 1.8;
    }

    h2, h3 {
      color: #ffba00;
      margin-top: 30px;
    }

    iframe {
      width: 100%;
      height: 400px;
      border: none;
      border-radius: 12px;
      margin: 20px 0;
    }

    .hidden {
      display: none;
    }

    .offer-btn {
      display: inline-block;
      margin-top: 20px;
      padding: 15px 30px;
      background-color: #ffba00;
      color: #000;
      font-weight: bold;
      text-decoration: none;
      border-radius: 8px;
      transition: background 0.3s;
    }

    .offer-btn:hover {
      background-color: #e0a800;
    }

    #timer {
      font-size: 24px;
      background: #222;
      padding: 10px 20px;
      text-align: center;
      border-radius: 8px;
      margin-bottom: 15px;
      color: #ffba00;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <h2>🚀 رحلتك لتعلم الطاقة الشمسية</h2>

  <div id="video1" class="video-block">
    <h3>📘 الفيديو الأول</h3>
    <iframe src="https://www.youtube.com/embed/VIDEO_ID_1" allowfullscreen></iframe>
  </div>

  <div id="video2" class="video-block hidden">
    <h3>📙 الفيديو الثاني</h3>
    <iframe src="https://www.youtube.com/embed/VIDEO_ID_2" allowfullscreen></iframe>
  </div>

  <div id="video3" class="video-block hidden">
    <h3>📗 الفيديو الثالث</h3>
    <iframe src="https://www.youtube.com/embed/VIDEO_ID_3" allowfullscreen></iframe>
  </div>

  <div id="offer" class="video-block hidden">
    <h3>🎁 العرض الخاص</h3>
    <div id="timer">00:00:00</div>
    <iframe src="https://www.youtube.com/embed/OFFER_VIDEO_ID" allowfullscreen></iframe>
    <a href="https://your-offer-link.com" class="offer-btn">سجل الآن</a>
  </div>

  <script>
    const startKey = "ovoStartDate";
    const offerKey = "offerStartTime";
    const today = new Date().setHours(0, 0, 0, 0);

    if (!localStorage.getItem(startKey)) {
      localStorage.setItem(startKey, today);
    }

    const startDate = parseInt(localStorage.getItem(startKey));
    const dayDiff = Math.floor((today - startDate) / (1000 * 60 * 60 * 24));

    if (dayDiff >= 0) document.getElementById("video1").classList.remove("hidden");
    if (dayDiff >= 1) document.getElementById("video2").classList.remove("hidden");
    if (dayDiff >= 2) document.getElementById("video3").classList.remove("hidden");

    if (dayDiff >= 3) {
      const offerDiv = document.getElementById("offer");
      offerDiv.classList.remove("hidden");

      // تعيين وقت بدء العرض لكل زائر
      if (!localStorage.getItem(offerKey)) {
        const offerStart = new Date().getTime();
        localStorage.setItem(offerKey, offerStart);
      }

      const offerStartTime = parseInt(localStorage.getItem(offerKey));
      const offerDuration = 24 * 60 * 60 * 1000; // 24 ساعة
      const offerEndTime = offerStartTime + offerDuration;

      const timerDiv = document.getElementById("timer");

      function updateTimer() {
        const now = new Date().getTime();
        const diff = offerEndTime - now;

        if (diff <= 0) {
          timerDiv.innerHTML = "⛔ انتهى وقت العرض";
          offerDiv.querySelector("iframe").remove();
          offerDiv.querySelector(".offer-btn").remove();
          clearInterval(timerInterval);
          return;
        }

        const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
        const minutes = Math.floor((diff / (1000 * 60)) % 60);
        const seconds = Math.floor((diff / 1000) % 60);

        timerDiv.innerHTML = `${hours.toString().padStart(2, '0')}:${minutes
          .toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
      }

      const timerInterval = setInterval(updateTimer, 1000);
      updateTimer();
    }
  </script>

</body>
<button onclick="resetAll()" style="
  position: fixed;
  bottom: 20px;
  left: 20px;
  padding: 10px 15px;
  font-size: 14px;
  background: red;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  z-index: 9999;
">🔄 إعادة ضبط الوقت (اختبار)</button>

<script>
  function resetAll() {
    localStorage.removeItem("ovoStartDate");
    localStorage.removeItem("offerStartTime");
    alert("✅ تم إعادة ضبط الوقت. أعد تحميل الصفحة لاختبار من البداية.");
    location.reload();
  }
</script>

</html>
# Free-Solar-Course
