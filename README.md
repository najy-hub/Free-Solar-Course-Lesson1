<!-- 🔻 كل الكود كما طلبت، مع إضافة منطق الردود في الأسفل فقط -->
<!-- لم يتم تغيير التنسيق الأساسي إطلاقًا -->

<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>رحلة المهندس المحترف</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Cairo', sans-serif; }

    body {
      background: linear-gradient(to right, #0f0f0f, #1c1c1c);
      color: #ffffff; line-height: 1.6;
    }

    header {
      padding: 20px 40px; background-color: #111111d0;
      display: flex; justify-content: space-between; align-items: center;
      border-bottom: 1px solid #333;
    }

    header h1 { font-size: 24px; color: #f9f9f9; }

    nav a {
      color: #ccc; text-decoration: none; margin-left: 20px; font-size: 16px;
      transition: color 0.3s;
    }

    nav a:hover { color: #ffffff; }

    .hero {
      position: relative;
      background-image: url('Images/hero.png');
      background-size: cover; background-position: center;
      height: 100vh;
      display: flex; align-items: center; justify-content: center;
      text-align: center;
    }

    .hero::after {
      content: ''; position: absolute; top: 0; left: 0;
      width: 100%; height: 100%; background-color: rgba(0,0,0,0.6); z-index: 1;
    }

    .hero-content {
      position: relative; z-index: 2;
      max-width: 800px; padding: 20px;
    }

    .hero h2 { font-size: 36px; margin-bottom: 20px; color: #ffffff; }
    .hero p { font-size: 18px; color: #dddddd; margin-bottom: 30px; }

    .hero a.button {
      padding: 12px 30px; background-color: #ffba00; color: #000;
      font-weight: bold; border: none; border-radius: 8px;
      text-decoration: none; font-size: 18px; transition: background-color 0.3s;
    }

    .hero a.button:hover { background-color: #ffaa00; }

    #video { padding: 60px 20px; text-align: center; }
    iframe { max-width: 100%; border-radius: 12px; }

    #comments-section {
      background-color: #111; padding: 40px 20px;
      max-width: 800px; margin: auto;
    }

    form {
      background: #1e1e1e; padding: 20px; border-radius: 10px;
      margin-bottom: 40px;
    }

    label { display: block; margin: 10px 0 5px; }

    input, textarea, select {
      width: 100%; padding: 10px; margin-bottom: 15px;
      border: none; border-radius: 8px;
      background: #2c2c2c; color: #fff;
    }

    button {
      background: #ffc107; color: #000;
      font-weight: bold; padding: 12px 20px;
      border: none; border-radius: 8px; cursor: pointer;
      transition: background 0.3s;
    }

    button:hover { background: #e0a800; }

    .comment-card {
      background-color: #1f1f1f; border: 1px solid #333;
      border-radius: 12px; padding: 15px;
      margin-bottom: 20px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    .comment-name { font-weight: bold; color: #ffba00; }
    .comment-stars { color: gold; }
    .comment-text { margin-top: 10px; color: #eee; line-height: 1.6; }

    .reply-card {
      background-color: #2a2a2a;
      margin-top: 10px; margin-right: 20px;
      border-left: 3px solid #ffba00;
      padding: 10px; border-radius: 8px;
    }

    footer {
      background-color: #101010;
      text-align: center; padding: 20px;
      color: #666; font-size: 14px;
      margin-top: 60px;
    }

    @media (max-width: 768px) {
      .hero h2 { font-size: 28px; }
      .hero p { font-size: 16px; }
      header { flex-direction: column; align-items: flex-start; }
      nav { margin-top: 10px; }
    }
  </style>
</head>
<body>

  <header>
    <h1>رحلة المهندس المحترف</h1>
    <nav>
      <a href="#video">فيديو</a>
      <a href="#comments-section">التعليقات</a>
    </nav>
  </header>

  <section class="hero">
    <div class="hero-content">
      <h2>رحلتك تبدأ من هنا</h2>
      <p>دورة متكاملة لتعلم تصميم وتنفيذ أنظمة الطاقة الشمسية بطرق عملية وعلمية.</p>
      <a href="#video" class="button">شاهد المقدمة</a>
    </div>
  </section>

  <section id="video">
    <h2 style="margin-bottom: 20px;">🎥 المحاضرة</h2>
    <iframe width="800" height="450"
      src="https://www.youtube.com/embed/zW9ZX-SZKtE"
      frameborder="0" allowfullscreen></iframe>
  </section>

  <section id="comments-section">
    <h2>💬 قسم التعليقات</h2>
    <form id="commentForm">
      <label>الاسم:</label>
      <input type="text" name="name" required>
      <label>البريد الإلكتروني (اختياري):</label>
      <input type="email" name="email">
      <label>التقييم:</label>
      <select name="rating">
        <option value="5">⭐️⭐️⭐️⭐️⭐️</option>
        <option value="4">⭐️⭐️⭐️⭐️</option>
        <option value="3">⭐️⭐️⭐️</option>
        <option value="2">⭐️⭐️</option>
        <option value="1">⭐️</option>
      </select>
      <label>التعليق:</label>
      <textarea name="comment" required></textarea>
      <input type="hidden" name="parentId" value="">
      <button type="submit">إرسال</button>
    </form>

    <div id="comments"></div>
  </section>

  <footer>
    &copy; 2025 جميع الحقوق محفوظة - رحلة المهندس المحترف
  </footer>

  <script>
    const scriptURL = "https://script.google.com/macros/s/AKfycby3WcuXOblJAmygxP84x707jO7B5f04ru2wILg8n1ax_9T4oZD4J05mDNbqIq-F45DK3A/exec";
    const adminEmail = "najycosa238@gmail.com"; // ← استبدله ببريدك (مستقبلاً يمكن تطويره لتسجيل دخول)

    document.getElementById("commentForm").addEventListener("submit", function(e) {
      e.preventDefault();
      const form = e.target;
      const formData = new FormData(form);

      fetch(scriptURL, {
        method: 'POST',
        body: formData
      }).then(() => {
        alert("✅ تم إرسال التعليق");
        form.reset();
        loadComments();
      });
    });

    function createCommentHtml(comment, replies) {
      const div = document.createElement("div");
      div.className = "comment-card";
      div.innerHTML = `
        <div class="comment-name">${comment.name}</div>
        <div class="comment-stars">${'⭐️'.repeat(comment.rating || 0)}</div>
        <div class="comment-text">${comment.comment}</div>
      `;

      const replyContainer = document.createElement("div");
      replies.forEach(reply => {
        const replyDiv = document.createElement("div");
        replyDiv.className = "reply-card";
        replyDiv.innerHTML = `<strong>${reply.name}:</strong> ${reply.comment}`;
        replyContainer.appendChild(replyDiv);
      });
      div.appendChild(replyContainer);

      // زر رد للمشرف فقط (يمكنك تفعيل شرط بالبريد لاحقًا)
      const replyBtn = document.createElement("button");
      replyBtn.textContent = "رد";
      replyBtn.style.marginTop = "10px";
      replyBtn.onclick = () => {
        const form = document.getElementById("commentForm");
        form.parentId.value = comment.rowId;
        form.scrollIntoView({ behavior: "smooth" });
      };
      div.appendChild(replyBtn);

      return div;
    }

    function loadComments() {
      fetch(scriptURL)
        .then(res => res.json())
        .then(data => {
          const commentSection = document.getElementById("comments");
          commentSection.innerHTML = "";

          const parents = data.filter(c => !c.parentId);
          const replies = data.filter(c => c.parentId);

          parents.reverse().forEach(parent => {
            const childReplies = replies.filter(r => r.parentId === parent.rowId);
            commentSection.appendChild(createCommentHtml(parent, childReplies));
          });
        });
    }

    window.onload = loadComments;
  </script>

</body>
</html>
