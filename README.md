 <!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>怡定瑶 · 时光纪念站</title>
  <style>
    /* ========== 全局变量与粉白蓝配色 ========== */
    :root {
      --bg-color: #FFFDFE; /* 极浅的暖白粉 */
      --card-bg: #FFFFFF;
      --text-main: #4A4A4A;
      --text-sub: #7A7A7A;
      --text-muted: #A0A0A0;
      
      /* 主色调：粉色系 */
      --color-pink-light: #FFD1DC;
      --color-pink-main: #FF9EBB;
      --color-pink-deep: #FF6B9E;
      
      /* 辅色调：清透蓝 */
      --color-blue-light: #DDF0F4;
      --color-blue-main: #AEC6CF;

      --gradient-main: linear-gradient(135deg, var(--color-pink-light) 0%, var(--color-pink-main) 100%);
      --shadow-soft: 0 8px 24px rgba(255, 158, 187, 0.12);
      --shadow-hover: 0 14px 28px rgba(255, 107, 158, 0.2);

      --font-serif: Georgia, "Times New Roman", "Songti SC", serif;
      --font-sans: -apple-system, BlinkMacSystemFont, "PingFang SC", "Helvetica Neue", sans-serif;
    }

    /* ========== 卡皮巴拉自定义光标 (适配浅色背景) ========== */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36' viewBox='0 0 36 36'%3E%3Cpath d='M6 18 C6 11 12 9 22 9 C26 9 29 11 29 14 C29 15.5 28 17 28 18 C30 19 31 21 30 24 C29 27 25 28 20 28 L10 28 C7 28 6 25 6 18 Z' fill='%23D4B896' stroke='%238D6E63' stroke-width='1.5' stroke-linejoin='round'/%3E%3Ccircle cx='24' cy='14' r='1.5' fill='%233E2723'/%3E%3Cpath d='M27 18 C26 19 25 19 24 18' stroke='%238D6E63' stroke-width='1.2' fill='none'/%3E%3Cellipse cx='18' cy='8' rx='1.8' ry='2.5' fill='%23D4B896' stroke='%238D6E63' stroke-width='1.2'/%3E%3C/svg%3E") 6 6, auto;
    }
    button, a, input, textarea, .timeline-item, .flip-card, .tab-btn {
      cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36' viewBox='0 0 36 36'%3E%3Cpath d='M6 18 C6 11 12 9 22 9 C26 9 29 11 29 14 C29 15.5 28 17 28 18 C30 19 31 21 30 24 C29 27 25 28 20 28 L10 28 C7 28 6 25 6 18 Z' fill='%23D4B896' stroke='%23FF9EBB' stroke-width='1.8' stroke-linejoin='round'/%3E%3Ccircle cx='24' cy='14' r='1.5' fill='%233E2723'/%3E%3Cpath d='M27 18 C26 19 25 19 24 18' stroke='%23FF9EBB' stroke-width='1.2' fill='none'/%3E%3Ccircle cx='20' cy='6' r='3' fill='%23FF9EBB' stroke='%23FFF' stroke-width='0.8'/%3E%3C/svg%3E") 6 6, pointer !important;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      font-family: var(--font-sans);
      line-height: 1.6;
      overflow-x: hidden;
      -webkit-font-smoothing: antialiased;
    }

    /* ========== 【一、开场动画：双手靠近 -> 十指相扣】 ========== */
    #intro-overlay {
      position: fixed;
      inset: 0;
      background: #FFFDFE;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 99999;
      transition: opacity 0.8s ease, visibility 0.8s;
    }
    #intro-overlay.hidden {
      opacity: 0;
      visibility: hidden;
      pointer-events: none;
    }

    .hands-animation-container {
      position: relative;
      width: 320px;
      height: 200px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* 阶段1：两只手靠近 */
    .hand-reach {
      position: absolute;
      width: 140px;
      height: 100px;
      opacity: 1;
      animation: handsMeet 2.5s cubic-bezier(0.25, 1, 0.5, 1) forwards;
    }
    
    .hand-reach-left {
      left: 0;
      /* 带有淡淡蓝色光晕的左手 */
      filter: drop-shadow(0 0 10px rgba(174, 198, 207, 0.6));
    }
    
    .hand-reach-right {
      right: 0;
      /* 带有淡淡粉色光晕的右手 */
      filter: drop-shadow(0 0 10px rgba(255, 158, 187, 0.6));
    }

    /* 阶段2：十指相扣 (初始隐藏，接触瞬间显示) */
    .hands-clasped {
      position: absolute;
      width: 180px;
      height: 140px;
      opacity: 0;
      transform: scale(0.9);
      filter: drop-shadow(0 0 20px rgba(255, 158, 187, 0.8));
      animation: claspReveal 2s ease forwards 2.4s;
    }

    .intro-text-group {
      position: absolute;
      top: 65%;
      text-align: center;
      opacity: 0;
      animation: textFadeIn 1.5s ease forwards 3s;
    }
    .intro-text-group h1 {
      font-family: var(--font-serif);
      font-size: 1.6rem;
      color: var(--color-pink-deep);
      letter-spacing: 0.2em;
      margin-bottom: 8px;
    }
    .intro-text-group p {
      font-size: 0.85rem;
      color: var(--color-blue-main);
      letter-spacing: 0.1em;
    }

    @keyframes handsMeet {
      0% { transform: translateX(calc(-100% * var(--dir))) translateY(20px); opacity: 0; }
      20% { opacity: 1; }
      95% { transform: translateX(calc(-10% * var(--dir))) translateY(0); opacity: 1; }
      100% { transform: translateX(calc(-5% * var(--dir))) translateY(0); opacity: 0; } /* 碰触瞬间隐藏 */
    }
    .hand-reach-left { --dir: -1; }
    .hand-reach-right { --dir: 1; }

    @keyframes claspReveal {
      0% { opacity: 0; transform: scale(0.95); }
      10% { opacity: 1; transform: scale(1.05); }
      100% { opacity: 1; transform: scale(1); }
    }
    @keyframes textFadeIn {
      to { opacity: 1; transform: translateY(-10px); }
    }

    /* ========== 顶部 Apple 风格磨砂导航 ========== */
    .apple-nav {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(15px);
      -webkit-backdrop-filter: blur(15px);
      border: 1px solid rgba(255, 158, 187, 0.3);
      box-shadow: 0 4px 20px rgba(255, 158, 187, 0.1);
      border-radius: 40px;
      padding: 6px 16px;
      display: flex;
      gap: 10px;
      z-index: 1000;
    }
    .nav-link {
      padding: 6px 14px;
      border-radius: 20px;
      font-size: 0.85rem;
      color: var(--text-sub);
      text-decoration: none;
      transition: all 0.3s ease;
    }
    .nav-link:hover { color: var(--color-pink-deep); background: var(--color-pink-light); }
    .nav-link.active { background: var(--color-pink-main); color: #FFF; font-weight: bold; }

    /* ========== 滚动 Reveal 动画 ========== */
    .main-container {
      max-width: 1000px;
      margin: 0 auto;
      padding: 120px 20px 80px;
    }
    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.8s ease, transform 0.8s ease;
    }
    .reveal.active { opacity: 1; transform: translateY(0); }

    /* 通用卡片与标题样式 */
    .section-block { margin-bottom: 100px; }
    .sec-title {
      font-family: var(--font-serif);
      font-size: 2rem;
      color: var(--color-pink-deep);
      text-align: center;
      margin-bottom: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
    }
    .sec-title::before, .sec-title::after {
      content: '';
      width: 40px;
      height: 2px;
      background: var(--color-pink-light);
    }
    .cp-card {
      background: var(--card-bg);
      border-radius: 20px;
      border: 1px solid rgba(255, 158, 187, 0.2);
      box-shadow: var(--shadow-soft);
      transition: all 0.4s ease;
    }
    .cp-card:hover {
      transform: translateY(-5px);
      box-shadow: var(--shadow-hover);
      border-color: var(--color-pink-main);
    }

    /* ========== 1. 首屏投稿箱 (保留并美化) ========== */
    .hero-section { text-align: center; margin-bottom: 80px; }
    .hero-title {
      font-family: var(--font-serif);
      font-size: 2.8rem;
      color: var(--text-main);
      margin-bottom: 10px;
    }
    .hero-title em { color: var(--color-pink-main); font-style: normal; }
    
    .mailbox {
      max-width: 600px;
      margin: 40px auto 0;
      padding: 30px;
      text-align: left;
    }
    .mailbox-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }
    .mailbox-header h3 { font-family: var(--font-serif); color: var(--color-pink-deep); }
    .btn-cloud {
      background: var(--color-blue-light);
      color: var(--color-blue-main);
      border: 1px solid var(--color-blue-main);
      padding: 5px 12px;
      border-radius: 20px;
      font-size: 0.8rem;
      transition: all 0.3s;
    }
    .btn-cloud:hover { background: var(--color-blue-main); color: #fff; }

    .mail-form input, .mail-form textarea {
      width: 100%;
      padding: 12px;
      border: 1px solid var(--color-pink-light);
      border-radius: 12px;
      background: #FFF;
      margin-bottom: 15px;
      font-family: inherit;
      outline: none;
      transition: border-color 0.3s;
    }
    .mail-form input:focus, .mail-form textarea:focus { border-color: var(--color-pink-main); }
    .mail-form textarea { resize: vertical; min-height: 80px; }
    
    .form-footer { display: flex; justify-content: space-between; align-items: center; }
    .anon-wrap { font-size: 0.85rem; color: var(--text-sub); display: flex; align-items: center; gap: 5px; }
    .btn-submit {
      background: var(--gradient-main);
      color: #FFF;
      border: none;
      padding: 8px 24px;
      border-radius: 20px;
      font-weight: bold;
    }

    /* ========== 2. 时光轴 (Timeline) ========== */
    .timeline { position: relative; padding: 20px 0; }
    .timeline::before {
      content: '';
      position: absolute;
      top: 0; bottom: 0; left: 24px;
      width: 2px;
      background: repeating-linear-gradient(to bottom, var(--color-pink-main) 0, var(--color-pink-main) 6px, transparent 6px, transparent 12px);
    }
    .timeline-item { position: relative; margin-bottom: 30px; padding-left: 60px; }
    .timeline-dot {
      position: absolute; left: 16px; top: 20px;
      width: 18px; height: 18px;
      border-radius: 50%;
      background: var(--color-pink-main);
      border: 3px solid #FFF;
      box-shadow: 0 0 0 2px var(--color-pink-light);
      transition: transform 0.3s;
    }
    .timeline-item:hover .timeline-dot { transform: scale(1.2); background: var(--color-pink-deep); }
    .timeline-content { padding: 20px 24px; }
    .timeline-content h4 { font-family: var(--font-serif); font-size: 1.1rem; color: var(--text-main); margin-bottom: 6px; }
    .timeline-date { font-size: 0.85rem; color: var(--color-blue-main); font-weight: bold; margin-bottom: 8px; display: block; }
    .timeline-desc { font-size: 0.9rem; color: var(--text-sub); }

    /* ========== 3. 双人百科 (About) ========== */
    .about-grid { display: flex; justify-content: space-between; align-items: center; gap: 20px; }
    .profile-card { flex: 1; padding: 30px; text-align: center; }
    .avatar-placeholder {
      width: 80px; height: 80px;
      margin: 0 auto 15px;
      border-radius: 50%;
      background: var(--color-pink-light);
      display: flex; align-items: center; justify-content: center;
      font-size: 2rem; color: #FFF;
    }
    .profile-card h3 { font-family: var(--font-serif); font-size: 1.5rem; color: var(--color-pink-deep); margin-bottom: 15px; }
    .info-row { display: flex; justify-content: space-between; font-size: 0.9rem; border-bottom: 1px dashed var(--color-pink-light); padding: 8px 0; }
    .quote-box { margin-top: 20px; padding: 10px; background: var(--bg-color); border-radius: 8px; font-style: italic; font-size: 0.85rem; color: var(--color-blue-main); }
    .connector { font-family: var(--font-serif); font-size: 2.5rem; color: var(--color-pink-main); font-style: italic; }

    /* ========== 4. 磕点名场面 (Highlights 3D) ========== */
    .highlights-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 24px; }
    .flip-card { perspective: 1000px; height: 180px; }
    .flip-inner {
      position: relative; width: 100%; height: 100%;
      transition: transform 0.6s; transform-style: preserve-3d;
    }
    .flip-card:hover .flip-inner { transform: rotateY(180deg); }
    .flip-front, .flip-back {
      position: absolute; inset: 0;
      backface-visibility: hidden;
      border-radius: 20px; padding: 25px;
      display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center;
    }
    .flip-front { background: var(--gradient-main); color: #FFF; }
    .flip-front h4 { font-family: var(--font-serif); font-size: 1.2rem; }
    .flip-back { transform: rotateY(180deg); background: #FFF; border: 2px solid var(--color-pink-light); color: var(--text-sub); font-size: 0.9rem; }

    /* ========== 5. 饭拍图库 (Gallery) ========== */
    .gallery-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; }
    .gallery-item { padding: 10px; }
    .gallery-img {
      aspect-ratio: 4/3;
      background: var(--color-blue-light);
      border-radius: 12px;
      display: flex; flex-direction: column; align-items: center; justify-content: center;
      color: var(--color-blue-main); font-size: 2rem; margin-bottom: 10px;
    }
    .gallery-caption { text-align: center; font-size: 0.9rem; font-family: var(--font-serif); color: var(--text-main); }

    /* ========== 6. 同人创作 (Fanworks) ========== */
    .tab-header { display: flex; justify-content: center; gap: 20px; margin-bottom: 30px; }
    .tab-btn { background: none; border: none; font-family: var(--font-serif); font-size: 1.1rem; color: var(--text-muted); padding-bottom: 5px; }
    .tab-btn.active { color: var(--color-pink-deep); border-bottom: 2px solid var(--color-pink-main); }
    .tab-content { display: none; grid-template-columns: repeat(2, 1fr); gap: 20px; }
    .tab-content.active { display: grid; }
    .fan-card { padding: 20px; }
    .fan-card h4 { font-family: var(--font-serif); color: var(--color-pink-deep); margin-bottom: 5px; }
    .fan-author { font-size: 0.8rem; color: var(--color-blue-main); margin-bottom: 10px; }
    .fan-desc { font-size: 0.85rem; color: var(--text-sub); }

    /* ========== 留言词云彩蛋 ========== */
    #cloud-modal {
      position: fixed; inset: 0; background: rgba(255, 253, 254, 0.95);
      z-index: 10000; display: none; opacity: 0; transition: opacity 0.5s;
    }
    #cloud-modal.active { display: block; opacity: 1; }
    #cloud-canvas { width: 100%; height: 100%; }
    .close-cloud {
      position: absolute; top: 20px; right: 30px;
      background: #FFF; border: 1px solid var(--color-pink-main); color: var(--color-pink-main);
      width: 40px; height: 40px; border-radius: 50%; font-size: 1.2rem; display: flex; align-items: center; justify-content: center; z-index: 2;
    }

    footer { text-align: center; padding: 40px; font-family: var(--font-serif); color: var(--text-muted); font-size: 0.9rem; }

    @media (max-width: 768px) {
      .apple-nav { width: 90%; justify-content: space-around; padding: 8px; }
      .about-grid, .highlights-grid, .gallery-grid, .tab-content { grid-template-columns: 1fr; }
      .connector { transform: rotate(90deg); margin: 10px 0; }
    }
  </style>
</head>
<body>

  <!-- ========== 【一、浪漫写实开场动画 (纯SVG模拟写实双手)】 ========== -->
  <div id="intro-overlay">
    <div class="hands-animation-container">
      
      <!-- 阶段1：左右手靠近 (使用具有立体感肤色和光影的 SVG Path) -->
      <!-- 左手 (带蓝色光晕) -->
      <svg class="hand-reach hand-reach-left" viewBox="0 0 200 150" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <linearGradient id="skinLeft" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stop-color="#FADCD9" />
            <stop offset="100%" stop-color="#F8B195" />
          </linearGradient>
        </defs>
        <!-- 简化的写实手臂与伸出的手指轮廓 -->
        <path d="M-20 90 C 40 80, 100 60, 150 70 C 170 75, 190 70, 195 65 C 198 62, 195 58, 190 60 C 170 65, 150 60, 140 50 C 130 40, 100 45, -20 60 Z" fill="url(#skinLeft)" stroke="#AEC6CF" stroke-width="2"/>
        <path d="M 140 50 C 160 55, 180 50, 185 45 C 188 42, 185 38, 180 40 C 160 45, 150 40, 140 40 Z" fill="url(#skinLeft)"/>
      </svg>

      <!-- 右手 (带粉色光晕) -->
      <svg class="hand-reach hand-reach-right" viewBox="0 0 200 150" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <linearGradient id="skinRight" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stop-color="#FFE0D2" />
            <stop offset="100%" stop-color="#F39C12" stop-opacity="0.5"/>
          </linearGradient>
        </defs>
        <path d="M220 90 C 160 80, 100 60, 50 70 C 30 75, 10 70, 5 65 C 2 62, 5 58, 10 60 C 30 65, 50 60, 60 50 C 70 40, 100 45, 220 60 Z" fill="url(#skinLeft)" stroke="#FF9EBB" stroke-width="2"/>
        <path d="M 60 50 C 40 55, 20 50, 15 45 C 12 42, 15 38, 20 40 C 40 45, 50 40, 60 40 Z" fill="url(#skinLeft)"/>
      </svg>

      <!-- 阶段2：十指相扣特写图 -->
      <svg class="hands-clasped" viewBox="0 0 300 200" xmlns="http://www.w3.org/2000/svg">
        <!-- 精致交叠的手指轮廓模拟十指相扣 -->
        <g fill="url(#skinLeft)" stroke="#FFF" stroke-width="2">
          <!-- 背景手腕 -->
          <path d="M 20 180 C 60 120, 100 80, 150 90 C 180 95, 200 110, 210 130 C 220 150, 200 180, 180 200 Z" opacity="0.9"/>
          <!-- 交错的手指 1 -->
          <path d="M 100 100 C 120 70, 150 60, 170 80 C 180 90, 170 110, 150 120 Z"/>
          <!-- 交错的手指 2 -->
          <path d="M 120 120 C 140 90, 170 80, 190 100 C 200 110, 190 130, 170 140 Z"/>
          <!-- 交错的手指 3 -->
          <path d="M 140 140 C 160 110, 190 100, 210 120 C 220 130, 210 150, 190 160 Z"/>
          <!-- 覆盖手腕 -->
          <path d="M 280 180 C 240 120, 200 80, 150 90 C 120 95, 100 110, 90 130 C 80 150, 100 180, 120 200 Z" opacity="0.9"/>
        </g>
        <!-- 相扣瞬间爆发的星星光芒 -->
        <circle cx="150" cy="110" r="4" fill="#FFF" filter="drop-shadow(0 0 10px #FF9EBB)"/>
        <path d="M 150 90 L 155 105 L 170 110 L 155 115 L 150 130 L 145 115 L 130 110 L 145 105 Z" fill="#FFF" filter="drop-shadow(0 0 5px #AEC6CF)"/>
      </svg>
    </div>

    <div class="intro-text-group">
      <h1>爱怡定瑶有回应</h1>
      <p>YI & YAO MEMORIAL</p>
    </div>
  </div>


  <!-- ========== 导航栏 ========== -->
  <nav class="apple-nav">
    <a href="#hero" class="nav-link active">寄语</a>
    <a href="#timeline" class="nav-link">时光</a>
    <a href="#about" class="nav-link">档案</a>
    <a href="#highlights" class="nav-link">名场面</a>
    <a href="#fanworks" class="nav-link">二创</a>
  </nav>


  <!-- ========== 主体内容 ========== -->
  <main class="main-container">
    
    <!-- 首屏：投稿箱 -->
    <section id="hero" class="hero-section reveal">
      <h1 class="hero-title">怡定瑶 <em>Memorial</em></h1>
      <p style="color:var(--text-sub); letter-spacing:0.1em;">“爱怡定瑶有回应”</p>

      <div class="cp-card mailbox">
        <div class="mailbox-header">
          <h3>💌 心声信箱</h3>
          <button class="btn-cloud" onclick="toggleCloud(true)">✨ 查看共鸣词云</button>
        </div>
        <form class="mail-form" onsubmit="submitMail(event)">
          <input type="text" id="m-name" placeholder="您的昵称 (选填)" maxlength="15">
          <textarea id="m-msg" placeholder="写下你想对怡定瑶说的祝福或心声..." required></textarea>
          <div class="form-footer">
            <label class="anon-wrap"><input type="checkbox" id="m-anon"> 匿名投递</label>
            <button type="submit" class="btn-submit">发送祝福</button>
          </div>
        </form>
      </div>
    </section>

    <!-- 时光轴 -->
    <section id="timeline" class="section-block reveal">
      <h2 class="sec-title">时光足迹</h2>
      <div class="timeline">
        <div class="timeline-item">
          <div class="timeline-dot"></div>
          <div class="cp-card timeline-content">
            <span class="timeline-date">2026.01.01</span>
            <h4>【此处替换为真实事件：初次相遇】</h4>
            <p class="timeline-desc">【此处替换为真实事件详情：记录两人初遇的具体时间、地点与美好瞬间】</p>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-dot"></div>
          <div class="cp-card timeline-content">
            <span class="timeline-date">2026.03.14</span>
            <h4>【此处替换为真实事件：出圈互动】</h4>
            <p class="timeline-desc">【此处替换为真实事件详情：记录两人在活动中的默契配合】</p>
          </div>
        </div>
        <div class="timeline-item">
          <div class="timeline-dot"></div>
          <div class="cp-card timeline-content">
            <span class="timeline-date">2026.08.08</span>
            <h4>【此处替换为真实事件：最新里程碑】</h4>
            <p class="timeline-desc">【此处替换为真实事件详情：记录最新的成就与感动时刻】</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 双人百科 -->
    <section id="about" class="section-block reveal">
      <h2 class="sec-title">双人百科</h2>
      <div class="about-grid">
        <div class="cp-card profile-card">
          <div class="avatar-placeholder">🌸</div>
          <h3>怡</h3>
          <div class="info-row"><span>昵称</span><span>【待替换】</span></div>
          <div class="info-row"><span>MBTI</span><span>【待替换】</span></div>
          <div class="quote-box">“【待替换：经典语录】”</div>
        </div>
        
        <div class="connector">&</div>

        <div class="cp-card profile-card">
          <div class="avatar-placeholder" style="background:var(--color-blue-main);">🌟</div>
          <h3 style="color:var(--color-blue-main);">瑶</h3>
          <div class="info-row"><span>昵称</span><span>【待替换】</span></div>
          <div class="info-row"><span>MBTI</span><span>【待替换】</span></div>
          <div class="quote-box" style="color:var(--color-pink-deep);">“【待替换：经典语录】”</div>
        </div>
      </div>
    </section>

    <!-- 磕点名场面 -->
    <section id="highlights" class="section-block reveal">
      <h2 class="sec-title">磕点名场面</h2>
      <div class="highlights-grid">
        <div class="flip-card">
          <div class="flip-inner">
            <div class="flip-front"><h4>名场面 1 号</h4></div>
            <div class="flip-back">【待替换：名场面1号详细描述】</div>
          </div>
        </div>
        <div class="flip-card">
          <div class="flip-inner">
            <div class="flip-front"><h4>名场面 2 号</h4></div>
            <div class="flip-back">【待替换：名场面2号详细描述】</div>
          </div>
        </div>
        <div class="flip-card">
          <div class="flip-inner">
            <div class="flip-front"><h4>名场面 3 号</h4></div>
            <div class="flip-back">【待替换：名场面3号详细描述】</div>
          </div>
        </div>
        <div class="flip-card">
          <div class="flip-inner">
            <div class="flip-front"><h4>名场面 4 号</h4></div>
            <div class="flip-back">【待替换：名场面4号详细描述】</div>
          </div>
        </div>
      </div>
    </section>

    <!-- 饭拍图库 -->
    <section id="gallery" class="section-block reveal">
      <h2 class="sec-title">饭拍精选</h2>
      <div class="gallery-grid">
        <div class="cp-card gallery-item">
          <div class="gallery-img">📸</div>
          <div class="gallery-caption">【待替换：图片描述 1】</div>
        </div>
        <div class="cp-card gallery-item">
          <div class="gallery-img">📸</div>
          <div class="gallery-caption">【待替换：图片描述 2】</div>
        </div>
      </div>
    </section>

    <!-- 同人创作 -->
    <section id="fanworks" class="section-block reveal">
      <h2 class="sec-title">同人创作</h2>
      <div class="tab-header">
        <button class="tab-btn active" onclick="switchTab('fan-text')">同人文</button>
        <button class="tab-btn" onclick="switchTab('fan-art')">同人画</button>
      </div>
      
      <div id="fan-text" class="tab-content active">
        <div class="cp-card fan-card">
          <h4>【待替换：文章标题 1】</h4>
          <div class="fan-author">作者：【待替换】</div>
          <div class="fan-desc">【待替换：内容简介...】</div>
        </div>
        <div class="cp-card fan-card">
          <h4>【待替换：文章标题 2】</h4>
          <div class="fan-author">作者：【待替换】</div>
          <div class="fan-desc">【待替换：内容简介...】</div>
        </div>
      </div>

      <div id="fan-art" class="tab-content">
        <div class="cp-card fan-card">
          <h4>【待替换：画作名称 1】</h4>
          <div class="fan-author">画手：【待替换】</div>
          <div class="fan-desc">【待替换：画作简介...】</div>
        </div>
      </div>
    </section>

  </main>

  <footer>
    💕 爱怡定瑶有回应 · 本站已陪伴 <span id="days-count" style="color:var(--color-pink-deep); font-weight:bold;">0</span> 天
  </footer>

  <!-- 词云彩蛋幕布 -->
  <div id="cloud-modal">
    <button class="close-cloud" onclick="toggleCloud(false)">×</button>
    <canvas id="cloud-canvas"></canvas>
  </div>


  <!-- ========== 脚本逻辑 ========== -->
  <script>
    // 1. 开场动画控制
    window.addEventListener('load', () => {
      setTimeout(() => {
        const overlay = document.getElementById('intro-overlay');
        overlay.classList.add('hidden');
      }, 4500); // 动画总时长4.5秒后消失
    });

    // 2. 滚动 Reveal 动画与导航高亮
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('active'); });
    }, { threshold: 0.1 });
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

    const navLinks = document.querySelectorAll('.apple-nav a');
    window.addEventListener('scroll', () => {
      let fromTop = window.scrollY + 150;
      navLinks.forEach(link => {
        let section = document.querySelector(link.hash);
        if (section && section.offsetTop <= fromTop && section.offsetTop + section.offsetHeight > fromTop) {
          navLinks.forEach(a => a.classList.remove('active'));
          link.classList.add('active');
        }
      });
    });

    // 平滑滚动
    navLinks.forEach(link => {
      link.addEventListener('click', function(e) {
        e.preventDefault();
        document.querySelector(this.hash).scrollIntoView({ behavior: 'smooth' });
      });
    });

    // 3. 同人创作 Tab 切换
    function switchTab(tabId) {
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      event.target.classList.add('active');
      document.getElementById(tabId).classList.add('active');
    }

    // 4. 天数计算 (自2026-01-01)
    const start = new Date('2026-01-01');
    document.getElementById('days-count').innerText = Math.max(0, Math.floor((new Date() - start)/(1000*3600*24)));

    // 5. 留言与动态词云
    const STORE_KEY = 'ydy_cp_messages';
    function getMsgs() {
      return JSON.parse(localStorage.getItem(STORE_KEY)) || ['爱怡定瑶有回应', '坚定', '双向奔赴', '永远相伴'];
    }
    
    function submitMail(e) {
      e.preventDefault();
      const isAnon = document.getElementById('m-anon').checked;
      const msg = document.getElementById('m-msg').value.trim();
      if(!msg) return;
      
      let msgs = getMsgs();
      msgs.push(msg);
      localStorage.setItem(STORE_KEY, JSON.stringify(msgs));
      
      document.getElementById('m-msg').value = '';
      if(!isAnon) document.getElementById('m-name').value = '';
      alert('心声已成功投递！');
    }

    // 词云逻辑
    let cloudCanvas, cloudCtx, cloudAnim, bubbles = [];
    function toggleCloud(show) {
      const modal = document.getElementById('cloud-modal');
      if(show) {
        modal.classList.add('active');
        initCloudCanvas();
      } else {
        modal.classList.remove('active');
        cancelAnimationFrame(cloudAnim);
      }
    }

    function initCloudCanvas() {
      cloudCanvas = document.getElementById('cloud-canvas');
      cloudCtx = cloudCanvas.getContext('2d');
      cloudCanvas.width = window.innerWidth;
      cloudCanvas.height = window.innerHeight;
      
      const texts = getMsgs();
      bubbles = texts.map(t => {
        const colors = ['#FF9EBB', '#FF6B9E', '#AEC6CF', '#FFD1DC'];
        return {
          t: t.length > 12 ? t.slice(0,10)+'...' : t,
          x: Math.random() * (cloudCanvas.width - 100) + 50,
          y: Math.random() * (cloudCanvas.height - 100) + 50,
          vx: (Math.random() - 0.5) * 1.2,
          vy: (Math.random() - 0.5) * 1.2,
          size: Math.random() * 14 + 16,
          color: colors[Math.floor(Math.random() * colors.length)]
        };
      });
      renderCloud();
    }

    function renderCloud() {
      cloudCtx.clearRect(0, 0, cloudCanvas.width, cloudCanvas.height);
      bubbles.forEach(b => {
        b.x += b.vx; b.y += b.vy;
        if(b.x < 20 || b.x > cloudCanvas.width - 20) b.vx *= -1;
        if(b.y < 30 || b.y > cloudCanvas.height - 30) b.vy *= -1;
        
        cloudCtx.save();
        cloudCtx.font = `bold ${b.size}px Georgia, serif`;
        cloudCtx.fillStyle = b.color;
        cloudCtx.fillText(b.t, b.x, b.y);
        cloudCtx.restore();
      });
      cloudAnim = requestAnimationFrame(renderCloud);
    }
    
    window.addEventListener('resize', () => {
      if(cloudCanvas && document.getElementById('cloud-modal').classList.contains('active')) {
        cloudCanvas.width = window.innerWidth;
        cloudCanvas.height = window.innerHeight;
      }
    });
  </script>
</body>
</html>
     --font-serif: "Songti SC", "Source Han Serif CN", Georgia, serif;
      --font-sans: -apple-system, BlinkMacSystemFont, "PingFang SC", "Helvetica Neue", sans-serif;
    }

    /* ========== 卡皮巴拉自定义光标 ========== */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36' viewBox='0 0 36 36'%3E%3Cpath d='M6 18 C6 11 12 9 22 9 C26 9 29 11 29 14 C29 15.5 28 17 28 18 C30 19 31 21 30 24 C29 27 25 28 20 28 L10 28 C7 28 6 25 6 18 Z' fill='%23CBAA9E' stroke='%23FF6699' stroke-width='1.5' stroke-linejoin='round'/%3E%3Ccircle cx='24' cy='14' r='1.5' fill='%233D3538'/%3E%3Cpath d='M27 18 C26 19 25 19 24 18' stroke='%23FF6699' stroke-width='1.2' fill='none'/%3E%3Cellipse cx='18' cy='8' rx='1.8' ry='2.5' fill='%23CBAA9E' stroke='%23FF6699' stroke-width='1.2'/%3E%3C/svg%3E") 6 6, auto;
    }

    button, a, input, textarea, .cp-card, .flip-card, .tab-btn {
      cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='36' height='36' viewBox='0 0 36 36'%3E%3Cpath d='M6 18 C6 11 12 9 22 9 C26 9 29 11 29 14 C29 15.5 28 17 28 18 C30 19 31 21 30 24 C29 27 25 28 20 28 L10 28 C7 28 6 25 6 18 Z' fill='%23CBAA9E' stroke='%23FF1493' stroke-width='1.8' stroke-linejoin='round'/%3E%3Ccircle cx='24' cy='14' r='1.5' fill='%233D3538'/%3E%3Cpath d='M27 18 C26 19 25 19 24 18' stroke='%23FF1493' stroke-width='1.2' fill='none'/%3E%3Ccircle cx='20' cy='6' r='3' fill='%23FFA6C2' stroke='%23FF1493' stroke-width='1'/%3E%3C/svg%3E") 6 6, pointer !important;
    }

    body {
      background-color: var(--bg-base);
      color: var(--text-main);
      font-family: var(--font-sans);
      overflow-x: hidden;
      line-height: 1.7;
    }

    /* ========== 图二精髓：粉笔涂鸦与毛边手写字体系统 ========== */
    .chalk-title {
      font-family: var(--font-chalk);
      color: var(--chalk-pink);
      text-shadow: 2px 2px 0px rgba(255, 255, 255, 0.9), 
                   -1px -1px 0px rgba(255, 102, 153, 0.4),
                   0 0 8px rgba(255, 102, 153, 0.3);
      letter-spacing: 0.05em;
      position: relative;
      display: inline-block;
      font-weight: 900;
    }

    .chalk-title::before {
      content: attr(data-text);
      position: absolute;
      left: 2px;
      top: 1px;
      color: #FFFFFF;
      z-index: -1;
      opacity: 0.8;
      filter: blur(0.5px);
    }

    /* ==========================================
       【一、1:1 复刻图一开场 6 大分镜动画】
       ========================================== */
    #intro-overlay {
      position: fixed;
      inset: 0;
      background: #040813;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 99999;
      overflow: hidden;
      animation: overlayFadeOut 1.0s cubic-bezier(0.16, 1, 0.3, 1) 9.8s forwards;
    }

    /* 满屏星光落雪 Canvas */
    #snow-stardust-canvas {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
    }

    /* 舞台主画框 */
    .story-stage-viewport {
      position: relative;
      width: 100vw;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2;
    }

    /* 分镜 1、2、3：双人从两侧走到中央牵手 */
    .shot-figures-wrap {
      position: absolute;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      animation: shotFiguresFade 0.6s ease 4.2s forwards;
    }

    /* 分镜 1->2：左侧身着白纱的人物逐步向右走 */
    .figure-actor-left {
      position: absolute;
      bottom: 22%;
      left: 14%;
      width: 160px;
      height: 260px;
      background: url('https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=400&q=80') center/cover no-repeat;
      mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 40%, rgba(0,0,0,0) 80%);
      -webkit-mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 40%, rgba(0,0,0,0) 80%);
      filter: brightness(0.9) contrast(1.1) drop-shadow(0 0 20px rgba(167, 199, 231, 0.8));
      animation: actorWalkLeft 3.6s cubic-bezier(0.25, 1, 0.5, 1) forwards;
    }

    /* 分镜 1->2：右侧身着礼服的人物逐步向左走 */
    .figure-actor-right {
      position: absolute;
      bottom: 22%;
      right: 14%;
      width: 160px;
      height: 260px;
      background: url('https://images.unsplash.com/photo-1517841905240-472988babdf9?auto=format&fit=crop&w=400&q=80') center/cover no-repeat;
      mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 40%, rgba(0,0,0,0) 80%);
      -webkit-mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 40%, rgba(0,0,0,0) 80%);
      filter: brightness(0.9) contrast(1.1) drop-shadow(0 0 20px rgba(255, 166, 194, 0.8));
      animation: actorWalkRight 3.6s cubic-bezier(0.25, 1, 0.5, 1) forwards;
    }

    /* 地面舞台云雾极光 */
    .stage-bottom-aurora {
      position: absolute;
      bottom: 16%;
      width: 70vw;
      height: 35px;
      border-radius: 50%;
      background: radial-gradient(ellipse, rgba(167, 199, 231, 0.9) 0%, rgba(255, 166, 194, 0.6) 40%, transparent 75%);
      filter: blur(12px);
    }

    /* 分镜 4 & 5：镜头无缝切换至双手相扣特写 */
    .shot-hands-closeup {
      position: absolute;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0;
      animation: handsCloseupShow 0.8s ease 4.3s forwards;
    }

    /* 真实写实双手特写交汇 */
    .hands-real-bg {
      position: relative;
      width: 550px;
      height: 320px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .hand-arm-left {
      position: absolute;
      left: -60px;
      width: 320px;
      height: 160px;
      background: linear-gradient(135deg, rgba(246, 229, 229, 0.95), rgba(221, 167, 165, 0.85));
      clip-path: polygon(0 40%, 65% 35%, 85% 45%, 100% 50%, 85% 65%, 65% 60%, 0 75%);
      filter: drop-shadow(0 0 15px rgba(167, 199, 231, 0.9));
      animation: handClaspMoveLeft 1.8s cubic-bezier(0.16, 1, 0.3, 1) 4.4s forwards;
    }

    .hand-arm-right {
      position: absolute;
      right: -60px;
      width: 320px;
      height: 160px;
      background: linear-gradient(225deg, rgba(255, 230, 235, 0.95), rgba(255, 166, 194, 0.85));
      clip-path: polygon(100% 40%, 35% 35%, 15% 45%, 0 50%, 15% 65%, 35% 60%, 100% 75%);
      filter: drop-shadow(0 0 15px rgba(255, 102, 153, 0.9));
      animation: handClaspMoveRight 1.8s cubic-bezier(0.16, 1, 0.3, 1) 4.4s forwards;
    }

    /* 分镜 5：掌心相聚处的星光爆发核心点 */
    .palm-starlight-core {
      position: absolute;
      width: 24px;
      height: 24px;
      border-radius: 50%;
      background: #FFFFFF;
      box-shadow: 0 0 35px 20px #86C7FE, 0 0 70px 40px #FF6699;
      opacity: 0;
      transform: scale(0);
      animation: palmGlowBurst 2.0s ease-out 5.6s forwards;
      z-index: 5;
    }

    /* 分镜 6：文字「爱怡定瑶有回应」浮现收尾（对标图二手写风） */
    .shot-slogan-reveal {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      z-index: 10;
      opacity: 0;
      animation: sloganRevealUp 1.4s cubic-bezier(0.16, 1, 0.3, 1) 6.8s forwards;
      white-space: nowrap;
    }

    .intro-chalk-slogan {
      font-family: var(--font-chalk);
      font-size: 4.2rem;
      color: #FFFFFF;
      text-shadow: 0 0 20px rgba(255, 102, 153, 0.9), 0 0 40px rgba(167, 199, 231, 0.8);
      letter-spacing: 0.15em;
      transform: rotate(-3deg);
    }

    .intro-sub-en {
      font-family: var(--font-serif);
      font-size: 0.85rem;
      letter-spacing: 0.4em;
      color: rgba(255, 255, 255, 0.85);
      margin-top: 12px;
    }

    @keyframes actorWalkLeft {
      to { left: 34%; }
    }
    @keyframes actorWalkRight {
      to { right: 34%; }
    }
    @keyframes shotFiguresFade {
      to { opacity: 0; visibility: hidden; }
    }
    @keyframes handsCloseupShow {
      to { opacity: 1; }
    }
    @keyframes handClaspMoveLeft {
      to { transform: translateX(70px) rotate(4deg); }
    }
    @keyframes handClaspMoveRight {
      to { transform: translateX(-70px) rotate(-4deg); }
    }
    @keyframes palmGlowBurst {
      0% { opacity: 0; transform: scale(0); }
      40% { opacity: 1; transform: scale(2.8); }
      100% { opacity: 0.7; transform: scale(1.6); }
    }
    @keyframes sloganRevealUp {
      from { opacity: 0; transform: translate(-50%, -40%) scale(0.9); }
      to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
    }
    @keyframes overlayFadeOut {
      to { opacity: 0; visibility: hidden; }
    }

    /* ==========================================
       【二、主体排版设计（图二粉色手写氛围）】
       ========================================== */
    .top-glass-nav {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255, 255, 255, 0.88);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid rgba(255, 102, 153, 0.35);
      box-shadow: 0 6px 24px rgba(255, 102, 153, 0.15);
      border-radius: 40px;
      padding: 8px 24px;
      display: flex;
      gap: 16px;
      z-index: 1000;
    }

    .nav-item {
      font-family: var(--font-chalk);
      font-size: 1.25rem;
      color: var(--text-sub);
      text-decoration: none;
      padding: 4px 14px;
      border-radius: 20px;
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .nav-item:hover, .nav-item.active {
      color: #FFFFFF;
      background: var(--chalk-pink);
      text-shadow: none;
      box-shadow: var(--shadow-pink-glow);
    }

    .main-wrapper {
      max-width: 1020px;
      margin: 0 auto;
      padding: 130px 24px 80px;
    }

    .scroll-reveal {
      opacity: 0;
      transform: translateY(35px);
      transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .scroll-reveal.active {
      opacity: 1;
      transform: translateY(0);
    }

    .section-box {
      margin-bottom: 120px;
    }

    .section-title-wrap {
      text-align: center;
      margin-bottom: 45px;
    }

    .sec-chalk-h2 {
      font-size: 2.8rem;
      display: inline-block;
      transform: rotate(-2deg);
    }

    .cp-card {
      background: var(--bg-card);
      border-radius: 20px;
      border: 1.5px solid rgba(255, 102, 153, 0.22);
      box-shadow: var(--shadow-card);
      transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), box-shadow 0.4s ease, border-color 0.3s ease;
    }
    .cp-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 16px 36px rgba(255, 102, 153, 0.22);
      border-color: var(--chalk-pink);
    }

    /* --- 1. 首屏专属投递信箱 --- */
    .hero-banner {
      text-align: center;
      margin-bottom: 90px;
    }

    .hero-title-chalk {
      font-size: 4.4rem;
      line-height: 1.1;
      margin-bottom: 16px;
      transform: rotate(-1.5deg);
    }

    .hero-subtitle {
      font-family: var(--font-chalk);
      font-size: 1.6rem;
      color: var(--text-sub);
    }

    .inbox-card-wrap {
      max-width: 650px;
      margin: 40px auto 0;
      padding: 36px;
      text-align: left;
    }

    .inbox-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 24px;
    }

    .inbox-header h3 {
      font-family: var(--font-chalk);
      font-size: 1.8rem;
      color: var(--chalk-pink);
    }

    .btn-cloud-spark {
      background: rgba(167, 199, 231, 0.25);
      border: 1.5px solid var(--color-sky-blue);
      color: #4676A9;
      font-family: var(--font-chalk);
      font-size: 1.1rem;
      padding: 6px 16px;
      border-radius: 25px;
      transition: all 0.3s ease;
    }
    .btn-cloud-spark:hover {
      background: var(--color-sky-blue);
      color: #FFFFFF;
      box-shadow: 0 0 12px rgba(167, 199, 231, 0.6);
    }

    .inbox-form {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .inbox-input, .inbox-textarea {
      width: 100%;
      padding: 14px 18px;
      border: 1.5px solid rgba(255, 102, 153, 0.3);
      border-radius: 14px;
      background: #FFFDFE;
      font-size: 0.95rem;
      font-family: inherit;
      color: var(--text-main);
      outline: none;
      transition: all 0.3s ease;
    }
    .inbox-input:focus, .inbox-textarea:focus {
      border-color: var(--chalk-pink);
      box-shadow: 0 0 0 4px rgba(255, 102, 153, 0.15);
      background: #FFFFFF;
    }
    .inbox-textarea {
      min-height: 90px;
      resize: vertical;
    }

    .inbox-bottom-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 6px;
    }
    .anon-label {
      font-family: var(--font-chalk);
      font-size: 1.15rem;
      color: var(--text-sub);
      display: flex;
      align-items: center;
      gap: 6px;
      user-select: none;
    }
    .anon-label input { accent-color: var(--chalk-pink); }

    .btn-send-mail {
      padding: 10px 28px;
      border-radius: 30px;
      background: var(--chalk-pink);
      color: #FFFFFF;
      border: none;
      font-family: var(--font-chalk);
      font-size: 1.3rem;
      letter-spacing: 0.05em;
      box-shadow: var(--shadow-pink-glow);
      transition: all 0.3s ease;
    }
    .btn-send-mail:hover {
      transform: scale(1.04);
      background: #FF4D88;
    }

    /* --- 2. 时光轴 --- */
    .timeline-track {
      position: relative;
      padding-left: 45px;
      margin-left: 20px;
      border-left: 2px dashed var(--chalk-pink);
    }
    .timeline-node {
      position: relative;
      margin-bottom: 40px;
    }
    .timeline-pin {
      position: absolute;
      left: -53px;
      top: 18px;
      width: 16px;
      height: 16px;
      border-radius: 50%;
      background: var(--chalk-pink);
      border: 3px solid #FFF;
      box-shadow: 0 0 0 3px rgba(255, 102, 153, 0.35);
    }
    .timeline-card {
      padding: 24px 28px;
    }
    .timeline-date-tag {
      font-family: var(--font-chalk);
      font-size: 1.4rem;
      color: var(--chalk-pink);
      margin-bottom: 6px;
      display: block;
    }
    .timeline-card h4 {
      font-family: var(--font-chalk);
      font-size: 1.5rem;
      color: var(--text-main);
      margin-bottom: 8px;
    }
    .timeline-card p {
      font-size: 0.92rem;
      color: var(--text-sub);
    }

    /* --- 3. 双人百科 --- */
    .about-pair-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 30px;
    }
    .profile-single-card {
      flex: 1;
      padding: 36px 28px;
      text-align: center;
    }
    .avatar-icon-bubble {
      width: 88px;
      height: 88px;
      border-radius: 50%;
      background: rgba(255, 102, 153, 0.15);
      border: 2px solid var(--chalk-pink);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.2rem;
      margin: 0 auto 18px;
      box-shadow: var(--shadow-pink-glow);
    }
    .profile-single-card h3 {
      font-family: var(--font-chalk);
      font-size: 2.2rem;
      color: var(--chalk-pink);
      margin-bottom: 16px;
    }
    .info-list-box {
      display: flex;
      flex-direction: column;
      gap: 10px;
      font-size: 0.92rem;
      margin-bottom: 18px;
    }
    .info-line {
      display: flex;
      justify-content: space-between;
      border-bottom: 1px dashed rgba(255, 102, 153, 0.3);
      padding-bottom: 6px;
    }
    .quote-hand-bubble {
      margin-top: 14px;
      padding: 12px;
      border-radius: 12px;
      background: #FFF5F8;
      font-family: var(--font-chalk);
      font-size: 1.25rem;
      color: var(--chalk-pink);
      border-left: 3px solid var(--chalk-pink);
    }
    .pair-amp-chalk {
      font-family: var(--font-chalk);
      font-size: 3.8rem;
      color: var(--color-sky-blue);
      transform: rotate(8deg);
      text-shadow: 0 0 10px rgba(167, 199, 231, 0.8);
    }

    /* --- 4. 磕点名场面 (3D 翻转) --- */
    .highlights-3d-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 24px;
    }
    .flip-3d-card {
      perspective: 1000px;
      height: 200px;
    }
    .flip-3d-inner {
      position: relative;
      width: 100%;
      height: 100%;
      transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
      transform-style: preserve-3d;
      border-radius: 20px;
    }
    .flip-3d-card:hover .flip-3d-inner {
      transform: rotateY(180deg);
    }
    .flip-3d-front, .flip-3d-back {
      position: absolute;
      inset: 0;
      backface-visibility: hidden;
      -webkit-backface-visibility: hidden;
      border-radius: 20px;
      padding: 24px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
    }
    .flip-3d-front {
      background: #FFFFFF;
      border: 1.5px solid rgba(255, 102, 153, 0.25);
      box-shadow: var(--shadow-card);
    }
    .flip-3d-front h4 {
      font-family: var(--font-chalk);
      font-size: 1.6rem;
      color: var(--chalk-pink);
    }
    .flip-3d-front .hint-txt {
      font-size: 0.75rem;
      color: var(--text-muted);
      margin-top: 8px;
    }
    .flip-3d-back {
      transform: rotateY(180deg);
      background: linear-gradient(135deg, #FFF0F5 0%, #FFE4ED 100%);
      border: 1.5px solid var(--chalk-pink);
      color: var(--text-main);
      font-size: 0.9rem;
      line-height: 1.6;
    }

    /* --- 5. 饭拍图库 --- */
    .gallery-photo-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 26px;
    }
    .gallery-photo-card {
      padding: 14px 14px 20px;
    }
    .gallery-photo-box {
      aspect-ratio: 16/10;
      background: linear-gradient(135deg, rgba(167, 199, 231, 0.3) 0%, rgba(255, 166, 194, 0.3) 100%);
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
      color: var(--chalk-pink);
      margin-bottom: 12px;
    }
    .gallery-photo-cap {
      font-family: var(--font-chalk);
      font-size: 1.35rem;
      text-align: center;
      color: var(--text-main);
    }

    /* --- 6. 同人二创 --- */
    .fan-tab-nav {
      display: flex;
      justify-content: center;
      gap: 30px;
      margin-bottom: 35px;
    }
    .fan-tab-btn {
      background: transparent;
      border: none;
      font-family: var(--font-chalk);
      font-size: 1.6rem;
      color: var(--text-muted);
      padding-bottom: 4px;
      transition: all 0.3s ease;
    }
    .fan-tab-btn.active {
      color: var(--chalk-pink);
      border-bottom: 3px solid var(--chalk-pink);
    }
    .fan-content-pane {
      display: none;
      grid-template-columns: repeat(2, 1fr);
      gap: 24px;
    }
    .fan-content-pane.active {
      display: grid;
    }
    .fan-work-card {
      padding: 28px;
    }
    .fan-work-card h4 {
      font-family: var(--font-chalk);
      font-size: 1.5rem;
      color: var(--chalk-pink);
      margin-bottom: 6px;
    }
    .fan-work-author {
      font-size: 0.82rem;
      color: var(--color-sky-blue);
      font-weight: bold;
      margin-bottom: 12px;
    }
    .fan-work-desc {
      font-size: 0.9rem;
      color: var(--text-sub);
      line-height: 1.6;
    }

    /* ========== 动态词云全屏彩蛋 ========== */
    #wordcloud-modal {
      position: fixed;
      inset: 0;
      background: rgba(255, 253, 254, 0.96);
      z-index: 10000;
      display: none;
      opacity: 0;
      transition: opacity 0.5s ease;
    }
    #wordcloud-modal.active {
      display: block;
      opacity: 1;
    }
    #cloud-canvas-full {
      width: 100%;
      height: 100%;
    }
    .btn-close-modal {
      position: absolute;
      top: 30px;
      right: 35px;
      width: 44px;
      height: 44px;
      border-radius: 50%;
      background: #FFFFFF;
      border: 1.5px solid var(--chalk-pink);
      color: var(--chalk-pink);
      font-size: 1.4rem;
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2;
      transition: all 0.3s ease;
    }
    .btn-close-modal:hover {
      background: var(--chalk-pink);
      color: #FFFFFF;
      transform: rotate(90deg);
    }

    /* ========== 页脚 ========== */
    footer {
      text-align: center;
      padding: 45px 20px;
      font-family: var(--font-chalk);
      font-size: 1.3rem;
      color: var(--text-muted);
      border-top: 1px dashed rgba(255, 102, 153, 0.3);
    }
    footer em {
      color: var(--chalk-pink);
      font-style: normal;
      font-size: 1.5rem;
    }

    /* ========== 响应式调整 ========== */
    @media (max-width: 860px) {
      .top-glass-nav { width: 92%; justify-content: space-around; padding: 6px 12px; }
      .nav-item { font-size: 1.1rem; padding: 4px 8px; }
      .about-pair-row, .highlights-3d-grid, .gallery-photo-grid, .fan-content-pane { grid-template-columns: 1fr; flex-direction: column; }
      .pair-amp-chalk { transform: rotate(90deg); margin: -10px 0; }
      .hero-title-chalk { font-size: 3.2rem; }
      .intro-chalk-slogan { font-size: 2.8rem; }
    }
  </style>
</head>
<body>

  <!-- ==========================================
       【一、1:1 复刻图一分镜动画层】
       ========================================== -->
  <div id="intro-overlay">
    <!-- 星空与落雪 Canvas -->
    <canvas id="snow-stardust-canvas"></canvas>

    <div class="story-stage-viewport">
      
      <!-- 分镜 1, 2, 3：双人从两侧走到中央牵手 -->
      <div class="shot-figures-wrap">
        <div class="figure-actor-left"></div>
        <div class="figure-actor-right"></div>
        <div class="stage-bottom-aurora"></div>
      </div>

      <!-- 分镜 4 & 5：双手交汇特写 + 星光相扣 -->
      <div class="shot-hands-closeup">
        <div class="hands-real-bg">
          <div class="hand-arm-left"></div>
          <div class="hand-arm-right"></div>
          <div class="palm-starlight-core"></div>
        </div>
      </div>

      <!-- 分镜 6：文字「爱怡定瑶有回应」浮现 -->
      <div class="shot-slogan-reveal">
        <div class="intro-chalk-slogan chalk-title" data-text="爱怡定瑶有回应">爱怡定瑶有回应</div>
        <div class="intro-sub-en">LOVE ALWAYS HAS A RESPONSE</div>
      </div>

    </div>
  </div>


  <!-- ==========================================
       【二、主体排版页面（对标图二手写风）】
       ========================================== -->
  
  <!-- 顶部玻璃导航 -->
  <nav class="top-glass-nav">
    <a href="#hero" class="nav-item active">寄语</a>
    <a href="#timeline" class="nav-item">时光</a>
    <a href="#about" class="nav-item">档案</a>
    <a href="#highlights" class="nav-item">名场面</a>
    <a href="#gallery" class="nav-item">光影</a>
    <a href="#fanworks" class="nav-item">二创</a>
  </nav>

  <main class="main-wrapper">
    
    <!-- 1. 信箱与 Hero -->
    <section id="hero" class="hero-banner scroll-reveal">
      <h1 class="hero-title-chalk chalk-title" data-text="爱怡定瑶有回应">爱怡定瑶有回应</h1>
      <p class="hero-subtitle">“坚定与回应，是双向奔赴最好的序章”</p>

      <div class="cp-card inbox-card-wrap">
        <div class="inbox-header">
          <h3>💌 心声共鸣信箱</h3>
          <button class="btn-cloud-spark" onclick="toggleCloudModal(true)">✨ 开启星海词云</button>
        </div>
        <form class="inbox-form" onsubmit="handleMailSubmit(event)">
          <input type="text" id="mail-name" class="inbox-input" placeholder="您的署名 / 昵称 (留空则匿名)" maxlength="15">
          <textarea id="mail-msg" class="inbox-textarea" placeholder="写下你想对怡定瑶说的祝福或心声..." required maxlength="240"></textarea>
          <div class="inbox-bottom-bar">
            <label class="anon-label"><input type="checkbox" id="mail-anon"> 匿名投递</label>
            <button type="submit" class="btn-send-mail">投递心愿 💕</button>
          </div>
        </form>
      </div>
    </section>

    <!-- 2. 时光轴板块 -->
    <section id="timeline" class="section-box scroll-reveal">
      <div class="section-title-wrap">
        <h2 class="sec-chalk-h2 chalk-title" data-text="时光足迹">时光足迹</h2>
      </div>
      <div class="timeline-track">
        <div class="timeline-node">
          <div class="timeline-pin"></div>
          <div class="cp-card timeline-card">
            <span class="timeline-date-tag">2026.01.01</span>
            <h4>【初次相遇 / 初舞台事件名称】</h4>
            <p>【此处替换为真实事件详情：记录两人初遇的具体时间、地点、舞台表现与幕后花絮等美好瞬间】</p>
          </div>
        </div>
        <div class="timeline-node">
          <div class="timeline-pin"></div>
          <div class="cp-card timeline-card">
            <span class="timeline-date-tag">2026.03.14</span>
            <h4>【白色情人节同台 / 出圈互动】</h4>
            <p>【此处替换为真实事件详情：记录两人在活动中的眼神对视、默契配合及经典名台词记录】</p>
          </div>
        </div>
        <div class="timeline-node">
          <div class="timeline-pin"></div>
          <div class="cp-card timeline-card">
            <span class="timeline-date-tag">2026.08.08</span>
            <h4>【周年纪念 / 最新里程碑】</h4>
            <p>【此处替换为真实事件详情：记录最新的共同成就与双向奔赴的感动时刻】</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 3. 双人百科档案 -->
    <section id="about" class="section-box scroll-reveal">
      <div class="section-title-wrap">
        <h2 class="sec-chalk-h2 chalk-title" data-text="双人百科档案">双人百科档案</h2>
      </div>
      <div class="about-pair-row">
        <!-- 怡 -->
        <div class="cp-card profile-single-card">
          <div class="avatar-icon-bubble">🌸</div>
          <h3>怡</h3>
          <div class="info-list-box">
            <div class="info-line"><span>昵称</span><span>【待替换：如小怡】</span></div>
            <div class="info-line"><span>MBTI</span><span>【待替换：如 ENFP】</span></div>
            <div class="info-line"><span>代表符号</span><span>【待替换：如 🌸】</span></div>
          </div>
          <div class="quote-hand-bubble">“【待替换：怡的经典语录或对瑶说过的暖心话】”</div>
        </div>

        <div class="pair-amp-chalk">&</div>

        <!-- 瑶 -->
        <div class="cp-card profile-single-card">
          <div class="avatar-icon-bubble" style="background:rgba(167,199,231,0.2); border-color:var(--color-sky-blue);">🌟</div>
          <h3 style="color:var(--color-sky-blue);">瑶</h3>
          <div class="info-list-box">
            <div class="info-line"><span>昵称</span><span>【待替换：如瑶瑶】</span></div>
            <div class="info-line"><span>MBTI</span><span>【待替换：如 INFJ】</span></div>
            <div class="info-line"><span>代表符号</span><span>【待替换：如 🌟】</span></div>
          </div>
          <div class="quote-hand-bubble" style="border-left-color:var(--color-sky-blue); color:#4676A9; background:#F0F8FF;">“【待替换：瑶的经典语录或对怡说过的暖心话】”</div>
        </div>
      </div>
    </section>

    <!-- 4. 磕点名场面 -->
    <section id="highlights" class="section-box scroll-reveal">
      <div class="section-title-wrap">
        <h2 class="sec-chalk-h2 chalk-title" data-text="磕点名场面">磕点名场面</h2>
      </div>
      <div class="highlights-3d-grid">
        <div class="flip-3d-card">
          <div class="flip-3d-inner">
            <div class="flip-3d-front">
              <h4>名场面 1 号</h4>
              <span class="hint-txt">（悬停翻转查看）</span>
            </div>
            <div class="flip-3d-back">
              【待替换：名场面1号的详细描述、现场气氛、高甜眼神与糖点解析】
            </div>
          </div>
        </div>
        <div class="flip-3d-card">
          <div class="flip-3d-inner">
            <div class="flip-3d-front">
              <h4>名场面 2 号</h4>
              <span class="hint-txt">（悬停翻转查看）</span>
            </div>
            <div class="flip-3d-back">
              【待替换：名场面2号的详细描述、现场气氛、高甜眼神与糖点解析】
            </div>
          </div>
        </div>
        <div class="flip-3d-card">
          <div class="flip-3d-inner">
            <div class="flip-3d-front">
              <h4>名场面 3 号</h4>
              <span class="hint-txt">（悬停翻转查看）</span>
            </div>
            <div class="flip-3d-back">
              【待替换：名场面3号的详细描述、现场气氛、高甜眼神与糖点解析】
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 5. 饭拍图库 -->
    <section id="gallery" class="section-box scroll-reveal">
      <div class="section-title-wrap">
        <h2 class="sec-chalk-h2 chalk-title" data-text="饭拍光影">饭拍光影</h2>
      </div>
      <div class="gallery-photo-grid">
        <div class="cp-card gallery-photo-card">
          <div class="gallery-photo-box">📸</div>
          <div class="gallery-photo-cap">【待替换：双人红毯瞬间】</div>
        </div>
        <div class="cp-card gallery-photo-card">
          <div class="gallery-photo-box">📸</div>
          <div class="gallery-photo-cap">【待替换：舞台抓拍对视】</div>
        </div>
      </div>
    </section>

    <!-- 6. 同人二创 -->
    <section id="fanworks" class="section-box scroll-reveal">
      <div class="section-title-wrap">
        <h2 class="sec-chalk-h2 chalk-title" data-text="同人二创">同人二创</h2>
      </div>
      <div class="fan-tab-nav">
        <button class="fan-tab-btn active" onclick="switchFanworksTab('fan-text')">📖 同人文</button>
        <button class="fan-tab-btn" onclick="switchFanworksTab('fan-art')">🎨 同人画</button>
      </div>

      <div id="fan-text" class="fan-content-pane active">
        <div class="cp-card fan-work-card">
          <h4>【待替换：同人文标题 1】</h4>
          <div class="fan-work-author">作者：【待替换】</div>
          <p class="fan-work-desc">【此处填写同人文内容简介或经典片段节选，字数适中...】</p>
        </div>
        <div class="cp-card fan-work-card">
          <h4>【待替换：同人文标题 2】</h4>
          <div class="fan-work-author">作者：【待替换】</div>
          <p class="fan-work-desc">【此处填写同人文内容简介或经典片段节选，字数适中...】</p>
        </div>
      </div>

      <div id="fan-art" class="fan-content-pane">
        <div class="cp-card fan-work-card">
          <h4>【待替换：插画名称 1】</h4>
          <div class="fan-work-author">画手：【待替换】</div>
          <p class="fan-work-desc">【此处填写插画主题概念阐述，如学院风日常、古风平行世界等...】</p>
        </div>
      </div>
    </section>

  </main>

  <!-- 页脚 -->
  <footer>
    💕 爱怡定瑶有回应 · 本站已记录 <em><span id="days-count">0</span></em> 天
  </footer>

  <!-- 动态词云全屏彩蛋幕布 -->
  <div id="wordcloud-modal">
    <button class="btn-close-modal" onclick="toggleCloudModal(false)">✕</button>
    <canvas id="cloud-canvas-full"></canvas>
  </div>


  <!-- ==========================================
       【三、JavaScript 逻辑与动画驱动】
       ========================================== -->
  <script>
    // 1. 绘制分镜星尘落雪 (Canvas)
    (function initStardustSnow() {
      const canvas = document.getElementById('snow-stardust-canvas');
      const ctx = canvas.getContext('2d');
      let w = canvas.width = window.innerWidth;
      let h = canvas.height = window.innerHeight;

      const particles = [];
      for (let i = 0; i < 160; i++) {
        particles.push({
          x: Math.random() * w,
          y: Math.random() * h,
          vx: (Math.random() - 0.5) * 0.6,
          vy: Math.random() * 1.8 + 0.8,
          s: Math.random() * 2.2 + 0.6,
          c: Math.random() > 0.4 ? '#FFFFFF' : (Math.random() > 0.5 ? '#FFA6C2' : '#A7C7E7'),
          a: Math.random() * 0.8 + 0.2
        });
      }

      function drawSnow() {
        ctx.clearRect(0, 0, w, h);
        particles.forEach(p => {
          p.x += p.vx;
          p.y += p.vy;
          if (p.y > h) { p.y = -10; p.x = Math.random() * w; }

          ctx.beginPath();
          ctx.arc(p.x, p.y, p.s, 0, Math.PI * 2);
          ctx.fillStyle = p.c;
          ctx.globalAlpha = p.a;
          ctx.shadowBlur = 6;
          ctx.shadowColor = p.c;
          ctx.fill();
        });
        requestAnimationFrame(drawSnow);
      }
      drawSnow();

      window.addEventListener('resize', () => {
        w = canvas.width = window.innerWidth;
        h = canvas.height = window.innerHeight;
      });
    })();

    // 2. 滚动监听与导航高亮
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) e.target.classList.add('active');
      });
    }, { threshold: 0.1 });
    document.querySelectorAll('.scroll-reveal').forEach(el => observer.observe(el));

    const navLinks = document.querySelectorAll('.top-glass-nav a');
    window.addEventListener('scroll', () => {
      let fromTop = window.scrollY + 180;
      navLinks.forEach(link => {
        let section = document.querySelector(link.hash);
        if (section && section.offsetTop <= fromTop && section.offsetTop + section.offsetHeight > fromTop) {
          navLinks.forEach(a => a.classList.remove('active'));
          link.classList.add('active');
        }
      });
    });

    navLinks.forEach(link => {
      link.addEventListener('click', function(e) {
        e.preventDefault();
        document.querySelector(this.hash).scrollIntoView({ behavior: 'smooth' });
      });
    });

    // 3. 同人创作 Tab 切换
    function switchFanworksTab(tabId) {
      document.querySelectorAll('.fan-tab-btn').forEach(b => b.classList.remove('active'));
      document.querySelectorAll('.fan-content-pane').forEach(c => c.classList.remove('active'));
      event.target.classList.add('active');
      document.getElementById(tabId).classList.add('active');
    }

    // 4. 计算天数 (2026-01-01 至今)
    const startDate = new Date('2026-01-01T00:00:00');
    document.getElementById('days-count').innerText = Math.max(0, Math.ceil((new Date() - startDate) / (1000 * 60 * 60 * 24)));

    // 5. 投递箱与动态词云
    const STORAGE_KEY = 'ydy_chalk_pink_mails';
    function getStoredMails() {
      return JSON.parse(localStorage.getItem(STORAGE_KEY)) || ['爱怡定瑶有回应', '浪漫永存', '坚定不移', '双向奔赴', '同频共振'];
    }

    function handleMailSubmit(e) {
      e.preventDefault();
      const isAnon = document.getElementById('mail-anon').checked;
      const msg = document.getElementById('mail-msg').value.trim();
      if (!msg) return;

      const mails = getStoredMails();
      mails.push(msg);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(mails));

      document.getElementById('mail-msg').value = '';
      if (!isAnon) document.getElementById('mail-name').value = '';
      alert('心愿已封存入星海！💕');
    }

    // 词云逻辑
    let cloudCanvas, cloudCtx, cloudAnim, bubbles = [];
    function toggleCloudModal(show) {
      const modal = document.getElementById('wordcloud-modal');
      if (show) {
        modal.classList.add('active');
        initCloudCanvas();
      } else {
        modal.classList.remove('active');
        cancelAnimationFrame(cloudAnim);
      }
    }

    function initCloudCanvas() {
      cloudCanvas = document.getElementById('cloud-canvas-full');
      cloudCtx = cloudCanvas.getContext('2d');
      cloudCanvas.width = window.innerWidth;
      cloudCanvas.height = window.innerHeight;

      const texts = getStoredMails();
      bubbles = texts.map(t => {
        const colors = ['#FF6699', '#FFA6C2', '#A7C7E7', '#3D3538'];
        return {
          t: t.length > 14 ? t.slice(0, 12) + '...' : t,
          x: Math.random() * (cloudCanvas.width - 160) + 50,
          y: Math.random() * (cloudCanvas.height - 100) + 50,
          vx: (Math.random() - 0.5) * 1.2,
          vy: (Math.random() - 0.5) * 1.2,
          size: Math.random() * 18 + 20,
          color: colors[Math.floor(Math.random() * colors.length)]
        };
      });
      renderWordCloud();
    }

    function renderWordCloud() {
      cloudCtx.clearRect(0, 0, cloudCanvas.width, cloudCanvas.height);
      bubbles.forEach(b => {
        b.x += b.vx;
        b.y += b.vy;
        if (b.x < 30 || b.x > cloudCanvas.width - 30) b.vx *= -1;
        if (b.y < 40 || b.y > cloudCanvas.height - 40) b.vy *= -1;

        cloudCtx.save();
        cloudCtx.font = `bold ${b.size}px "Caveat", "Kaiti SC", cursive`;
        cloudCtx.fillStyle = b.color;
        cloudCtx.shadowBlur = 6;
        cloudCtx.shadowColor = "rgba(255, 102, 153, 0.35)";
        cloudCtx.fillText(b.t, b.x, b.y);
        cloudCtx.restore();
      });
      cloudAnim = requestAnimationFrame(renderWordCloud);
    }

    window.addEventListener('resize', () => {
      if (cloudCanvas && document.getElementById('wordcloud-modal').classList.contains('active')) {
        cloudCanvas.width = window.innerWidth;
        cloudCanvas.height = window.innerHeight;
      }
    });
  </script>
</body>
</html>
```
