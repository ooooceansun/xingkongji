<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>星空纪民谣音乐酒馆 - 每日抽奖活动</title>
  <style>
    body {
      font-family: 'Microsoft YaHei', sans-serif;
      background-color: #1a1a2e;
      color: #fff;
      margin: 0;
      padding: 0;
      background-image: url('https://images.unsplash.com/photo-1606761568499-5cd0c2b96394'); /* 星空图，可替换 */
      background-size: cover;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      background-color: rgba(0, 0, 0, 0.7);
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
      margin-bottom: 30px;
      color: #f8c537;
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
    button:hover {
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
    .loading, .error, .result {
      text-align: center;
      margin: 10px 0;
      display: none;
    }
    .error {
      color: #ff6b6b;
    }
    .result {
      font-size: 20px;
      font-weight: bold;
    }
    .win {
      color: #f8c537;
    }
    .lose {
      color: #ccc;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>星空纪民谣音乐酒馆</h1>
    <div class="prize">每日抽奖：价值198元豪华威士忌套餐</div>
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

      <div class="loading" id="loading">正在抽奖，请稍候...</div>
      <div class="error" id="error"></div>
      <div class="result" id="result"></div>

      <button type="submit">立即参与抽奖</button>
    </form>

    <div class="rules">
      <h3>活动规则：</h3>
      <ul>
        <li>每日抽奖一次，立即出结果</li>
        <li>每日产生20位幸运顾客</li>
        <li>中奖结果将直接显示在页面</li>
        <li>奖品为价值198元豪华威士忌套餐</li>
        <li>中奖后请截图凭结果到店领取</li>
        <li>每人每天限参与一次</li>
      </ul>
    </div>

    <footer>
      © 2023 星空纪民谣音乐酒馆 保留所有权利
    </footer>
  </div>

  <script>
    document.getElementById('lotteryForm').addEventListener('submit', async function (e) {
      e.preventDefault();

      const name = document.getElementById('name').value.trim();
      const phone = document.getElementById('phone').value.trim();
      const errorElement = document.getElementById('error');
      const loadingElement = document.getElementById('loading');
      const resultElement = document.getElementById('result');

      errorElement.style.display = 'none';
      resultElement.style.display = 'none';

      if (!name || !phone) {
        showError('姓名和电话不能为空');
        return;
      }

      if (!/^1[3-9]\d{9}$/.test(phone)) {
        showError('请输入有效的手机号码');
        return;
      }

      loadingElement.style.display = 'block';

      await new Promise(resolve => setTimeout(resolve, 1000)); // 模拟抽奖延迟

      loadingElement.style.display = 'none';

      const isWinner = Math.random() < 0.1; // 10% 中奖率（可调整）

      if (isWinner) {
        resultElement.innerHTML = `<span class="win">🎉 恭喜您 ${name}，中奖了！请截图此页面到店领取奖品。</span>`;
      } else {
        resultElement.innerHTML = `<span class="lose">很遗憾，您未中奖，欢迎明日再来参与！</span>`;
      }

      resultElement.style.display = 'block';
      document.getElementById('lotteryForm').reset();

      function showError(message) {
        errorElement.textContent = message;
        errorElement.style.display = 'block';
        loadingElement.style.display = 'none';
      }
    });
  </script>
</body>
</html>
