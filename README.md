<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>怡定瑶 · 爱怡定瑶有回应</title>
  <style>
    /* ========== 全局配色与图二风格手写质感变量 ========== */
    :root {
      --bg-base: #FFFDFE;
      --bg-card: #FFFFFF;
      --text-main: #3D3538;
      --text-sub: #7A6E73;
      --text-muted: #A89FA3;
      
      /* 图二提取：纯正手绘亮粉与浅粉 */
      --chalk-pink: #FF6699;
      --chalk-pink-light: #FFA6C2;
      --chalk-white: #FFFFFF;
      --color-sky-blue: #A7C7E7;
      --color-deep-blue: #0B132B;
      
      --shadow-pink-glow: 0 0 12px rgba(255, 102, 153, 0.4);
      --shadow-card: 0 10px 30px rgba(255, 102, 153, 0.12);

      --font-chalk: "Caveat", "Kaiti SC", "STKaiti", "Comic Sans MS", cursive, sans-serif;
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
