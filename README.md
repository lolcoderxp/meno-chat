<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Nexus AI - Exact Layout & 3D Glass UI</title>
  <link href="https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css" rel="stylesheet" />
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Vazirmatn', -apple-system, sans-serif;
      -webkit-tap-highlight-color: transparent;
      -webkit-user-select: none;
      user-select: none;
    }

    body {
      background-color: #000000;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      overflow: hidden;
      position: relative;
    }

    /* --- هدر بالا (کاملاً تطبیق‌یافته با عکس اول: دکمه چت، دکمه دریافت پلاس و منو) --- */
    .top-header {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 20px;
      background: transparent;
      z-index: 100;
    }

    .header-left-group {
      display: flex;
      align-items: center;
    }

    .header-right-group {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    /* دکمه‌های دایره‌ای بالا با لایه نرم و سه بعدی */
    .header-circle-btn {
      position: relative;
      width: 46px;
      height: 46px;
      border-radius: 50%;
      background: linear-gradient(135deg, #161618 0%, #0a0a0c 100%);
      border: 1.5px solid rgba(255, 255, 255, 0.16);
      border-top: 1.5px solid rgba(255, 255, 255, 0.32);
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      color: #ffffff;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.85), inset 0 1px 3px rgba(255, 255, 255, 0.25);
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .header-circle-btn::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: 50%;
      background: linear-gradient(180deg, rgba(255,255,255,0.12) 0%, transparent 60%);
      pointer-events: none;
    }

    .header-circle-btn:hover {
      background: linear-gradient(135deg, #222226 0%, #111113 100%);
      transform: scale(1.06) translateY(-1px);
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.95), inset 0 1px 4px rgba(255, 255, 255, 0.35);
      border-color: rgba(255, 255, 255, 0.35);
    }

    /* دکمه "دریافت پلاس" با استایل دقیق عکس اول و لایه سه بعدی نرم */
    .header-pill-btn {
      position: relative;
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 10px 22px;
      background: linear-gradient(135deg, #161618 0%, #0a0a0c 100%);
      border: 1.5px solid rgba(255, 255, 255, 0.16);
      border-top: 1.5px solid rgba(255, 255, 255, 0.32);
      border-radius: 30px;
      cursor: pointer;
      color: #bfa1ff;
      font-size: 14px;
      font-weight: 500;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.85), inset 0 1px 3px rgba(255, 255, 255, 0.25);
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .header-pill-btn::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: 30px;
      background: linear-gradient(180deg, rgba(255,255,255,0.12) 0%, transparent 60%);
      pointer-events: none;
    }

    .header-pill-btn:hover {
      background: linear-gradient(135deg, #222226 0%, #111113 100%);
      color: #d8c4ff;
      transform: scale(1.04) translateY(-1px);
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.95), inset 0 1px 4px rgba(255, 255, 255, 0.35);
      border-color: rgba(255, 255, 255, 0.35);
    }

    /* --- ناحیه نمایش پیام‌ها --- */
    .chat-stream {
      flex-grow: 1;
      overflow-y: auto;
      padding: 84px 16px 20px 16px;
      display: flex;
      flex-direction: column;
      gap: 20px;
      scroll-behavior: smooth;
    }

    .chat-stream::-webkit-scrollbar {
      width: 4px;
    }

    .chat-stream::-webkit-scrollbar-thumb {
      background: rgba(255, 255, 255, 0.15);
      border-radius: 4px;
    }

    .message-row {
      display: flex;
      width: 100%;
      animation: fadeInMessage 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
    }

    @keyframes fadeInMessage {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .message-row.user {
      justify-content: flex-end;
    }

    .message-row.ai {
      justify-content: flex-start;
    }

    .message-bubble {
      max-width: 78%;
      padding: 12px 16px;
      font-size: 14.5px;
      line-height: 1.6;
      word-break: break-word;
      letter-spacing: -0.2px;
    }

    .message-row.user .message-bubble {
      background: #111113;
      color: #ffffff;
      border-radius: 20px 20px 4px 20px;
      border: 1px solid rgba(255, 255, 255, 0.1);
    }

    .message-row.ai .message-bubble {
      background: transparent;
      color: #e5e5ea;
      border-radius: 20px 20px 20px 4px;
      padding-right: 0;
    }

    /* --- پنل پایین (مطابق چیدمان دقیق عکس دوم: دکمه آبی صدا سمت چپ، میکروفون، متن و علامت پلاس سمت راست) --- */
    .footer-container {
      padding: 12px 16px 24px 16px;
      background: #000000;
      z-index: 100;
    }

    .chat-input-bar {
      position: relative;
      display: flex;
      align-items: center;
      background: #000000;
      border: 1.5px solid rgba(255, 255, 255, 0.18);
      border-top: 1.5px solid rgba(255, 255, 255, 0.32);
      border-radius: 32px;
      padding: 8px 14px;
      width: 100%;
      max-width: 768px;
      margin: 0 auto;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 1), inset 0 1px 3px rgba(255, 255, 255, 0.22);
    }

    .chat-input-bar::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: 32px;
      background: linear-gradient(180deg, rgba(255,255,255,0.08) 0%, transparent 50%);
      pointer-events: none;
    }

    /* بخش چپ باکس پایین (دکمه آبی صدا و میکروفون) */
    .bar-left-controls {
      display: flex;
      align-items: center;
      gap: 8px;
      flex-shrink: 0;
      z-index: 2;
    }

    /* دکمه آبی صدا (دقیقاً مشابه عکس دوم) با لایه سه بعدی نرم */
    .audio-mode-btn {
      position: relative;
      background: linear-gradient(135deg, #2b7de9 0%, #1752b0 100%);
      border: 1.5px solid rgba(255, 255, 255, 0.25);
      border-top: 1.5px solid rgba(255, 255, 255, 0.45);
      width: 42px;
      height: 42px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      border-radius: 50%;
      color: #ffffff;
      box-shadow: 0 6px 20px rgba(27, 115, 232, 0.45), inset 0 1px 3px rgba(255, 255, 255, 0.35);
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .audio-mode-btn::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: 50%;
      background: linear-gradient(180deg, rgba(255,255,255,0.25) 0%, transparent 60%);
      pointer-events: none;
    }

    .audio-mode-btn:hover {
      transform: scale(1.08) translateY(-1px);
      box-shadow: 0 10px 25px rgba(27, 115, 232, 0.65), inset 0 1px 4px rgba(255, 255, 255, 0.45);
    }

    /* دکمه میکروفون با ظاهر سه بعدی نرم */
    .bar-action-btn {
      position: relative;
      background: linear-gradient(135deg, #161618 0%, #0a0a0c 100%);
      border: 1.5px solid rgba(255, 255, 255, 0.14);
      border-top: 1.5px solid rgba(255, 255, 255, 0.28);
      width: 40px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      color: #98989f;
      border-radius: 50%;
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.8), inset 0 1px 2px rgba(255, 255, 255, 0.2);
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
      flex-shrink: 0;
    }

    .bar-action-btn::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: 50%;
      background: linear-gradient(180deg, rgba(255,255,255,0.1) 0%, transparent 60%);
      pointer-events: none;
    }

    .bar-action-btn:hover {
      background: linear-gradient(135deg, #222226 0%, #111113 100%);
      color: #ffffff;
      transform: scale(1.06) translateY(-1px);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.95), inset 0 1px 3px rgba(255, 255, 255, 0.3);
      border-color: rgba(255, 255, 255, 0.3);
    }

    /* فیلد ورودی متن امن و تک‌خطی */
    .chat-input {
      flex-grow: 1;
      background: transparent;
      border: none;
      outline: none;
      color: #ffffff;
      font-size: 15px;
      line-height: 40px;
      height: 40px;
      padding: 0 12px;
      direction: rtl;
      z-index: 2;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .chat-input::placeholder {
      color: #727278;
    }
  </style>
</head>
<body oncontextmenu="return false;">

  <header class="top-header">
    <div class="header-left-group">
      <button class="header-circle-btn" title="چت جدید">
        <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
          <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"></path>
        </svg>
      </button>
    </div>

    <div class="header-right-group">
      <button class="header-pill-btn" title="دریافت پلاس">
        <span>دریافت پلاس</span>
        <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 2l2.4 7.2L22 12l-7.6 2.8L12 22l-2.4-7.2L2 12l7.6-2.8L12 2z"></path>
        </svg>
      </button>

      <button class="header-circle-btn" title="منو">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="4" y1="7" x2="20" y2="7"></line>
          <line x1="4" y1="17" x2="20" y2="17"></line>
        </svg>
      </button>
    </div>
  </header>

  <div class="chat-stream" id="chatStream">
    <div class="message-row ai">
      <div class="message-bubble">
        طراحی منوی پایین دقیقا مطابق عکس ارسالی شما (دکمه صوتی آبی، میکروفون، فیلتر متن و دکمه پلاس) تنظیم شد و تمامی عناصر دارای لایه نرم و سه‌بعدیِ شیشه‌ای هستند.
      </div>
    </div>
  </div>

  <div class="footer-container">
    <div class="chat-input-bar">
      <div class="bar-left-controls">
        <button class="audio-mode-btn" title="حالت صوتی">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="20" x2="18" y2="10"></line>
            <line x1="12" y1="20" x2="12" y2="4"></line>
            <line x1="6" y1="20" x2="6" y2="14"></line>
          </svg>
        </button>

        <button class="bar-action-btn" title="میکروفون">
          <svg width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"></path>
            <path d="M19 10v1a7 7 0 0 1-14 0v-1"></path>
            <line x1="12" y1="19" x2="12" y2="23"></line>
            <line x1="8" y1="23" x2="16" y2="23"></line>
          </svg>
        </button>
      </div>

      <input type="text" class="chat-input" id="chatInput" placeholder="از ChatGPT بپرسید" autocomplete="off">

      <button class="bar-action-btn" title="پیوست یا افزودن">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="12" y1="5" x2="12" y2="19"></line>
          <line x1="5" y1="12" x2="19" y2="12"></line>
        </svg>
      </button>
    </div>
  </div>

</body>
</html>
