<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>星空纪民谣音乐酒馆 - 每日抽奖活动</title>
  <style>
    body {
      margin: 0;
      font-family: 'Microsoft YaHei', sans-serif;
      color: #fff;
      position: relative;
      min-height: 100vh;
      z-index: 0;
    }

    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0;
      width: 100%;
      height: 100%;
      background-image: url('2c1a24c3-ae81-4a2d-856b-4ddd8b0633bd.png');
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      z-index: -1;
      opacity: 0.8;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      background-color: rgba(0, 0, 0, 0.75);
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
      margin-top: 50px;
    }

    h1 {
      text-align: center;
      color: #f8c537;
      margin-bottom: 30px;
    }

    .prize {
      text-align: center;
      font-size: 24px;
      margin-bottom: 10px;
      color: #f8c537;
    }

    .prize-img {
      display: flex;
      justify-content: center;
      margin-bottom: 30px;
    }

    .prize-img img {
      max-width: 300px;
      border-radius: 10px;
      box-shadow: 0 0 10px #fff3;
    }

    .time {
      text-align: center;
      font-size: 18px;
      margin-bottom: 30px;
    }

    .form-group {
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 5px;
    }

    input {
      width: 100%;
      padding: 10px;
      border-radius: 5px;
      border: none;
      background-color: rgba(255, 255, 255, 0.9);
    }

    button {
      background-color: #f8c537;
      color: #000;
      border: none;
      padding: 12px 30px;
      font-size: 18px;
      border-radius: 5px;
      cursor: pointer;
      display: block;
      margin: 0 auto;
      transition: all 0.3s;
    }

    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    button:hover:not(:disabled) {
      background-color: #ffd700;
      transform: scale(1.05);
    }

    .rules {
      margin-top: 30px;
      padding: 15px;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 5px;
    }

    footer {
      text-align: center;
      margin-top: 30px;
      font-size: 14px;
      color: #aaa;
    }

    .loading {
      display: none;
      text-align: center;
      margin: 10px 0;
    }

    .error {
      color: #ff6b6b;
      text-align: center;
      margin: 10px 0;
      display: none;
    }

    .blocked {
      text-align: center;
      margin-top: 100px;
      font-size: 24px;
      color: red;
      display: none;
    }
  </style>
</head>
<body>
  <div class="container" id="mainContainer">
    <h1>星空纪民谣音乐酒馆</h1>
    <div class="prize">每日抽奖：价值198元豪华威士忌套餐</div>
    <div class="prize-img">
      <img src="62b32c46-fba5-4249-89d8-f4cd9b0e6826.jpg" alt="奖品图">
    </div>
    <div class="time">每日开奖时间：下午5点 · 每日20位幸运顾客</div>
    
    <form id="lotteryForm">
      <div class="form-group">
        <label for="name">您的姓名：</label>
        <input type="text" id="name" name="name" required />
      </div>
      <div class="form-group">
        <label for="phone">联系电话：</label>
        <input type="tel" id="phone" name="phone" required />
      </div>

      <div class="loading" id="loading">提交中，请稍候...</div>
      <div class="error" id="error"></div>

      <button type="submit" id="submitBtn">立即参与抽奖</button>
    </form>

    <div class="rules">
      <h3>活动规则：</h3>
      <ul>
        <li>每日抽奖一次，开奖时间为下午5点</li>
        <li>每日产生20位幸运顾客</li>
        <li>中奖者将当场显示中奖结果</li>
        <li>奖品为价值198元豪华威士忌套餐</li>
        <li>中奖后请在3天内凭页面截图到店领取</li>
        <li>每人每天限参与一次</li>
      </ul>
    </div>

    <footer>
      © 2023 星空纪民谣音乐酒馆 保留所有权利
    </footer>
  </div>

  <div class="blocked" id="blockedMessage">
    ⚠️ 访问被拒绝：检测到异常行为。请稍后再试。
  </div>

  <script>
    let lastSubmitTime = 0;
    const cooldown = 10000; // 10 秒冷却期
    let suspicious = false;

    document.getElementById('lotteryForm').addEventListener('submit', function (e) {
      e.preventDefault();

      const now = Date.now();
      const name = document.getElementById('name').value.trim();
      const phone = document.getElementById('phone').value.trim();
      const errorEl = document.getElementById('error');
      const loadingEl = document.getElementById('loading');
      const button = document.getElementById('submitBtn');

      // 恶意行为拦截
      if (suspicious) {
        document.getElementById('mainContainer').style.display = 'none';
        document.getElementById('blockedMessage').style.display = 'block';
        return;
      }

      // 防重复点击
      if (now - lastSubmitTime < cooldown) {
        showError("请勿频繁提交表单");
        suspicious = true;
        return;
      }

      // 验证格式
      if (!name || !phone) {
        showError('姓名和电话不能为空');
        return;
      }

      if (!/^1[3-9]\d{9}$/.test(phone)) {
        showError('请输入有效的手机号');
        return;
      }

      // 模拟抽奖逻辑
      loadingEl.style.display = 'block';
      errorEl.style.display = 'none';
      button.disabled = true;

      setTimeout(() => {
        const win = Math.random() < 0.2; // 20% 概率中奖
        alert(win ? "🎉 恭喜中奖！请截图此页面到店领取奖品！" : "感谢参与！今天未中奖，欢迎明天再试～");
        document.getElementById('lotteryForm').reset();
        button.disabled = false;
        loadingEl.style.display = 'none';
        lastSubmitTime = Date.now();
      }, 1200);

      function showError(msg) {
        errorEl.textContent = msg;
        errorEl.style.display = 'block';
        loadingEl.style.display = 'none';
      }
    });
  </script>
</body>
</html>
