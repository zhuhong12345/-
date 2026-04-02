<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>北木资源库 - 卡密验证</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            a: '#0f52ba',
            b: '#f5f5f5',
            c: '#333333',
            d: '#666666'
          },
          fontFamily: {
            sans: ['PingFang SC', 'Microsoft YaHei', 'sans-serif']
          }
        }
      }
    }
  </script>
  <style type="text/tailwindcss">
    @layer utilities {
      .x { box-shadow: 0 2px 8px rgba(0,0,0,0.08); }
      .y { background-color: rgba(15,82,186,0.05); }
      .z { max-height: 0; overflow: hidden; transition: max-height .3s ease; }
      .z.o { max-height: 300px; }
    }
  </style>
  <style>
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0,0,0,0.7);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
    }
    .modal {
      background: #2d2d2d;
      width: 80%;
      max-width: 400px;
      border-radius: 12px;
      padding: 24px;
      box-sizing: border-box;
      text-align: center;
    }
    .modal-title {
      color: #fff;
      font-size: 18px;
      margin: 0 0 32px;
      font-weight: 500;
    }
    .card-input {
      width: 100%;
      height: 48px;
      background: #3a3a3a;
      border: 1px solid #444;
      border-radius: 8px;
      color: #fff;
      padding: 0 12px;
      box-sizing: border-box;
      font-size: 16px;
      transition: border-color .3s;
    }
    .card-input::placeholder { color: #888; }
    .card-input:focus { outline: none; border-color: #409eff; }
    .error-tip {
      height: 20px;
      line-height: 20px;
      font-size: 14px;
      color: #f56c6c;
      margin-bottom: 24px;
      opacity: 0;
      transition: opacity .3s;
    }
    .error-tip.show { opacity: 1; }
    .success-tip {
      color: #67c23a;
      font-size: 16px;
      margin: 20px 0;
      display: none;
    }
    .modal-actions { display: flex; justify-content: space-between; }
    .modal-btn {
      width: 48%;
      height: 44px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color .3s;
    }
    .cancel-btn {
      background: transparent;
      color: #409eff;
      border: 1px solid #409eff;
    }
    .cancel-btn:hover { background: rgba(64,158,255,0.1); }
    .confirm-btn { background: #409eff; color: #fff; }
    .confirm-btn:disabled { background: #8cc5ff; cursor: not-allowed; }
    .resource-content { display: none; }
    .expire-tip {
      position: fixed;
      top: 10px;
      right: 10px;
      background: #409eff;
      color: #fff;
      padding: 8px 12px;
      border-radius: 6px;
      font-size: 14px;
      z-index: 999;
      box-shadow: 0 2px 10px rgba(64, 158, 255, 0.3);
    }
  </style>
</head>
<body class="bg-gray-100 min-h-screen">
  <div class="modal-overlay" id="modalOverlay">
    <div class="modal">
      <h3 class="modal-title">请输入卡密</h3>
      <div class="input-container">
        <input type="text" class="card-input" placeholder="请输入卡密:91" />
      </div>
      <div class="error-tip" id="errorTip">卡密错误，请重新输入</div>
      <div class="success-tip" id="successTip">验证通过！8小时内无需重复验证</div>
      <div class="modal-actions">
        <button class="modal-btn cancel-btn">取消</button>
        <button class="modal-btn confirm-btn" id="confirmBtn">确定</button>
      </div>
    </div>
  </div>

  <div class="expire-tip" id="expireTip" style="display: none;"></div>

  <div class="resource-content" id="resourceContent">
    <div class="bg-white rounded-xl mx-4 mt-4 p-4 x">
      <div class="flex items-center">
        <img src="1768953712907.png" alt="" class="w-14 h-14 rounded-full mr-3 border-2 border-a/20">
        <div>
          <h1 class="text-[clamp(1.2rem,3vw,1.5rem)] font-bold text-c">木北资源库</h1>
          <p class="text-sm text-d">每天更新资源，有问题欢迎加群反馈！1051104087</p>
        </div>
      </div>
    </div>
    <div class="bg-white rounded-xl mx-4 mt-4 p-4 x">
      <h2 class="text-base font-semibold text-c mb-3">默认功能</h2>
      <div class="grid grid-cols-2 gap-3">
        <a href="v.html" target="_blank" class="bg-a text-white py-2.5 rounded-lg font-medium transition-all hover:bg-a/90 text-center block">服务器监控</a>
        <a href="https://www.123684.com/s/re26Vv-wzcWd" target="_blank" class="bg-a text-white py-2.5 rounded-lg font-medium transition-all hover:bg-a/90 text-center block">弱网.apk下载</a>
      </div>
    </div>
    <div class="space-y-3 mx-4 mt-4 mb-8">
      <div class="bg-white rounded-xl p-4 x transition-all hover:y">
        <div class="flex items-center justify-between t cursor-pointer">
          <span class="text-base font-medium text-c">和平精英</span>
          <i class="fa fa-chevron-right text-d text-sm transition-transform duration-300"></i>
        </div>
        <div class="z mt-2 pl-4 space-y-2">
          <a href="https://www.123684.com/s/re26Vv-QzcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">功能pak</a>
          <a href="https://www.123684.com/s/re26Vv-EzcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">端口</a>
          <a href="https://www.123684.com/s/re26Vv-ozcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">美化</a>
          <a href="https://www.123684.com/s/re26Vv-kzcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">配置</a>
        </div>
      </div>
      <div class="bg-white rounded-xl p-4 x transition-all hover:y">
        <div class="flex items-center justify-between t cursor-pointer">
          <span class="text-base font-medium text-c">PUBG</span>
          <i class="fa fa-chevron-right text-d text-sm transition-transform duration-300"></i>
        </div>
        <div class="z mt-2 pl-4 space-y-2">
          <a href="https://www.123684.com/s/re26Vv-mzcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">功能Pak</a>
          <a href="https://www.123684.com/s/re26Vv-1zcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">美化pak</a>
          <a href="https://www.123684.com/s/re26Vv-4zcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">美化obb</a>
          <a href="https://example.com/mods" target="_blank" class="block py-2 text-d hover:text-a transition-colors">空</a>
        </div>
      </div>
      <div class="bg-white rounded-xl p-4 x transition-all hover:y">
        <div class="flex items-center justify-between t cursor-pointer">
          <span class="text-base font-medium text-c">三角洲</span>
          <i class="fa fa-chevron-right text-d text-sm transition-transform duration-300"></i>
        </div>
        <div class="z mt-2 pl-4 space-y-2">
          <a href="https://www.123684.com/s/re26Vv-xzcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">pak+配置</a>
          <a href="https://example.com/mods" target="_blank" class="block py-2 text-d hover:text-a transition-colors">空</a>
          <a href="https://example.com/mods" target="_blank" class="block py-2 text-d hover:text-a transition-colors">空</a>
        </div>
      </div>
      <div class="bg-white rounded-xl p-4 x transition-all hover:y">
        <div class="flex items-center justify-between t cursor-pointer">
          <span class="text-base font-medium text-c">暗区</span>
          <i class="fa fa-chevron-right text-d text-sm transition-transform duration-300"></i>
        </div>
        <div class="z mt-2 pl-4 space-y-2">
          <a href="https://www.123684.com/s/re26Vv-fzcWd" target="_blank" class="block py-2 text-d hover:text-a transition-colors">pak+配置</a>
        </div>
      </div>
    </div>
  </div>

    <script>
    (function(window, document) {
      const CONFIG = {
        VALID_CARDS: ['91', '', ''],
        VALID_HASHES: [
          '3e25960a79dbc69b674cd4ec67a72c6295d8e2b0ff9d327b648f6238f5d86e0f',
          'a87ff679a2f3e71d9181a67b7542122c225442955fb8c934458c98c3c92e3bbd',
          'f6cde2a0f819314cdde55fc227d8d7da9982a662f9c6b67dd800a416c100402e'
        ],
        ERROR_MSG: '卡密错误，请重新输入',
        EMPTY_MSG: '请输入卡密',
        VERIFY_KEY: 'card_verify_status',
        EXPIRE_HOURS: 8,
        expireTip: document.getElementById('expireTip')
      };

      // DOM 元素
      const modalOverlay = document.getElementById('modalOverlay');
      const resourceContent = document.getElementById('resourceContent');
      const cancelBtn = document.querySelector('.cancel-btn');
      const confirmBtn = document.getElementById('confirmBtn');
      const cardInput = document.querySelector('.card-input');
      const errorTip = document.getElementById('errorTip');
      const successTip = document.getElementById('successTip');

      window.onload = function() {
        checkVerifyStatus();
        initResourceToggle();
      };

      function checkVerifyStatus() {
        const verifyData = JSON.parse(localStorage.getItem(CONFIG.VERIFY_KEY));
        if (verifyData && verifyData.expireTime > Date.now()) {
          showResourceContent();
          startExpireTimer(verifyData.expireTime);
        }
      }

      async function sha256Encrypt(text) {
        try {
          const encoder = new TextEncoder();
          const data = encoder.encode(text);
          const digest = await window.crypto.subtle.digest('SHA-256', data);
          return Array.from(new Uint8Array(digest))
            .map(byte => byte.toString(16).padStart(2, '0'))
            .join('');
        } catch (e) {
          return null;
        }
      }

      async function verifyCard(code) {
        const hash = await sha256Encrypt(code);
        if (hash && CONFIG.VALID_HASHES.includes(hash)) {
          return true;
        }
        return CONFIG.VALID_CARDS.includes(code);
      }

      function showResourceContent() {
        modalOverlay.style.display = 'none';
        resourceContent.style.display = 'block';
      }

      function saveVerifyStatus() {
        const expireTime = Date.now() + CONFIG.EXPIRE_HOURS * 60 * 60 * 1000;
        localStorage.setItem(CONFIG.VERIFY_KEY, JSON.stringify({
          verified: true,
          expireTime: expireTime
        }));
        startExpireTimer(expireTime);
      }

      function formatTime(seconds) {
        const h = Math.floor(seconds / 3600);
        const m = Math.floor((seconds % 3600) / 60);
        const s = Math.floor(seconds % 60);
        return `${h.toString().padStart(2, '0')}:${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
      }

      function startExpireTimer(expireTime) {
        function updateTimer() {
          const now = Date.now();
          const remaining = expireTime - now;
          
          if (remaining <= 0) {
            CONFIG.expireTip.style.display = 'none';
            localStorage.removeItem(CONFIG.VERIFY_KEY);
            location.reload();
            return;
          }

          const remainingSeconds = remaining / 1000;
          CONFIG.expireTip.textContent = `倒计时结束，需要重新验证: ${formatTime(remainingSeconds)}`;
          CONFIG.expireTip.style.display = 'block';
        }

        updateTimer();
        setInterval(updateTimer, 1000);
      }

      function initResourceToggle() {
        document.querySelectorAll('.t').forEach(n => {
          const e = n.nextElementSibling;
          const t = n.querySelector('i');
          n.addEventListener('click', () => {
            e.classList.toggle('o');
            t.classList.toggle('rotate-90');
          });
        });
        document.querySelectorAll('.z a').forEach(n => {
          n.addEventListener('click', n => { n.stopPropagation(); });
        });
      }

      cancelBtn.addEventListener('click', () => {
        window.close();
      });

      confirmBtn.addEventListener('click', async function() {
        const inputCode = cardInput.value.trim();
        const btn = this;

        if (!inputCode) {
          errorTip.textContent = CONFIG.EMPTY_MSG;
          errorTip.classList.add('show');
          return;
        }

        errorTip.classList.remove('show');
        btn.disabled = true;
        btn.textContent = '验证中...';

        try {
          const isValid = await verifyCard(inputCode);
          if (isValid) {
            saveVerifyStatus();
            successTip.style.display = 'block';
            setTimeout(() => {
              showResourceContent();
            }, 1000);
          } else {
            errorTip.textContent = CONFIG.ERROR_MSG;
            errorTip.classList.add('show');
          }
        } catch (e) {
          errorTip.textContent = '验证异常，请重试';
          errorTip.classList.add('show');
        } finally {
          btn.disabled = false;
          btn.textContent = '确定';
        }
      });

      cardInput.addEventListener('focus', () => {
        errorTip.classList.remove('show');
      });

      cardInput.addEventListener('keydown', (e) => {
        if (e.key === 'Enter' && !confirmBtn.disabled) {
          confirmBtn.click();
        }
      });

    })(window, document);
  </script>
</body>
</html>
