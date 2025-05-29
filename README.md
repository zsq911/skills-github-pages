<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NG娱乐平台首页</title>
  <style>
    body {
      margin: 0;
      background: #111;
      font-family: sans-serif;
    }

    .notice-bar {
      display: flex;
      align-items: center;
      background: #003153;
      color: #fff;
      padding: 4px 10px;
      font-size: 14px;
    }

    .notice-icon {
      margin-right: 8px;
      animation: shake 1s infinite;
    }

    .notice-marquee-wrapper {
      overflow: hidden;
      flex: 1;
    }

    .notice-marquee {
      display: inline-block;
      white-space: nowrap;
      animation: marquee 15s linear infinite;
      padding-left: 100%;
    }

    @keyframes marquee {
      0% { transform: translateX(0); }
      100% { transform: translateX(-100%); }
    }

    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-3px); }
      75% { transform: translateX(3px); }
    }

    @keyframes shakeLR {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-5px); }
      75% { transform: translateX(5px); }
    }

    .shake-img {
      animation: shake 0.6s infinite;
    }

    .shake-left-right {
      animation: shakeLR 0.6s infinite;
    }

    .carousel-container {
      position: relative;
      overflow: hidden;
      max-width: 1000px;
      margin: 0 auto;
    }

    .carousel-track {
      display: flex;
      transition: transform 0.5s ease-in-out;
    }

    .carousel-slide {
      min-width: 100%;
    }

    .carousel-slide img {
      width: 100%;
      display: block;
    }

    .carousel-buttons {
      position: absolute;
      top: 50%;
      width: 100%;
      display: flex;
      justify-content: space-between;
      transform: translateY(-50%);
      pointer-events: none;
    }

    .carousel-buttons button {
      background: rgba(0, 0, 0, 0.5);
      color: white;
      border: none;
      padding: 10px;
      cursor: pointer;
      pointer-events: all;
    }

    .bottom-buttons {
      text-align: center;
      background: #000;
    }

    .bottom-buttons a {
      display: block;
    }

    .bottom-buttons img {
      width: 100%;
      display: block;
    }

    /* 金币爆炸动画样式 */
    .gold-coin {
      position: absolute;
      font-size: 24px;
      animation: coin-burst 1s ease-out forwards;
      pointer-events: none;
    }

    @keyframes coin-burst {
      0% {
        opacity: 1;
        transform: translate(0, 0) scale(1);
      }
      100% {
        opacity: 0;
        transform: translate(var(--x), var(--y)) scale(0.6);
      }
    }
  </style>
</head>
<body>

  <!-- 通知栏 -->
  <div class="notice-bar">
    <div class="notice-icon">🔊</div>
    <div class="notice-marquee-wrapper">
      <div class="notice-marquee">
        欢迎光临 NG娱乐平台！祝您好运连连，畅玩到底！🎉🧧💰
      </div>
    </div>
  </div>

  <!-- 轮播图 -->
  <div class="carousel-container">
    <div class="carousel-track" id="carouselTrack">
      <div class="carousel-slide"><img src="https://s21.ax1x.com/2025/05/29/pVpdCqg.jpg" alt="Banner 1" /></div>
      <div class="carousel-slide"><img src="https://s21.ax1x.com/2025/05/29/pVpdCqg.jpg" alt="Banner 2" /></div>
      <div class="carousel-slide"><img src="https://s21.ax1x.com/2025/05/29/pVpdCqg.jpg" alt="Banner 3" /></div>
    </div>
    <div class="carousel-buttons">
      <button onclick="moveSlide(-1)">‹</button>
      <button onclick="moveSlide(1)">›</button>
    </div>
  </div>

  <!-- 底部按钮区域 -->
  <div class="bottom-buttons" id="bottomButtons"></div>

  <!-- 脚本部分 -->
  <script>
    // 自动轮播
    const track = document.getElementById('carouselTrack');
    const slides = document.querySelectorAll('.carousel-slide');
    let index = 0;
    let autoSlide = setInterval(() => moveSlide(1), 3000);

    function moveSlide(direction) {
      index = (index + direction + slides.length) % slides.length;
      track.style.transform = `translateX(-${index * 100}%)`;
    }

    // 图片按钮数据
    const buttonsData = [
      { url: "https://imgse.com/i/pVpd1o9", img: "https://s21.ax1x.com/2025/05/29/pVpd1o9.png", alt: "底部按钮1" },
      { url: "https://wxjump.paradisemall.net/app/register.php?site_id=800&topId=577994", img: "https://s21.ax1x.com/2025/05/29/pVpdGJ1.jpg", alt: "底部按钮2", class: "shake-img" },
      { url: "https://156.234.96.4:60009/#/link?invite=7842128", img: "https://s21.ax1x.com/2025/05/29/pVpdwee.jpg", alt: "底部按钮3", class: "shake-img" },
      { url: "https://8118.pw/pg.html", img: "https://s21.ax1x.com/2025/05/29/pVp0ZuT.jpg", alt: "底部按钮新增7", class: "shake-left-right" },
      { url: "https://t.me/NG8866COM", img: "https://s21.ax1x.com/2025/05/29/pVpwW1x.jpg", alt: "Telegram", class: "shake-left-right" },
    ];

    const bottomContainer = document.getElementById("bottomButtons");

    buttonsData.forEach(({ url, img, alt, class: imgClass = "" }) => {
      const a = document.createElement("a");
      a.href = url;
      a.target = "_blank";
      a.rel = "noopener noreferrer";

      const image = document.createElement("img");
      image.src = img;
      image.alt = alt;
      image.loading = "lazy";
      if (imgClass) image.className = imgClass;

      a.appendChild(image);
      bottomContainer.appendChild(a);
    });

    // 💰 金币点击爆炸效果
    document.addEventListener("click", function (e) {
      for (let i = 0; i < 6; i++) {
        const coin = document.createElement("div");
        coin.className = "gold-coin";
        coin.textContent = "💰";

        const angle = Math.random() * 2 * Math.PI;
        const radius = 60 + Math.random() * 40;
        const offsetX = Math.cos(angle) * radius;
        const offsetY = Math.sin(angle) * radius;

        coin.style.left = `${e.pageX}px`;
        coin.style.top = `${e.pageY}px`;
        coin.style.setProperty('--x', `${offsetX}px`);
        coin.style.setProperty('--y', `${offsetY}px`);
        coin.style.fontSize = `${20 + Math.random() * 15}px`;

        document.body.appendChild(coin);
        setTimeout(() => coin.remove(), 1000);
      }
    });
  </script>
</body>
</html>
