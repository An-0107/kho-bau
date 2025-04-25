<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Đảo Kho Báu</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      color: white;
      text-align: center;
      background-size: cover;
    }
    .menu {
      display: flex;
      justify-content: center;
      margin: 10px;
      gap: 10px;
    }
    .menu button {
      padding: 10px 20px;
      font-size: 18px;
      cursor: pointer;
    }
    .info {
      position: fixed;
      top: 10px;
      left: 10px;
      background: rgba(0,0,0,0.6);
      padding: 10px;
      border-radius: 10px;
    }
    .shop-item {
      margin: 20px;
    }
    .shop-item img {
      width: 100px;
      height: auto;
    }
    .chest {
      width: 200px;
      margin-top: 50px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <div class="info">
    Số kim cương: <span id="diamonds">0</span> 💎<br>
    Vật dụng: <span id="item">Xẻng gỗ</span><br>
    Số lần đào: <span id="digs">0</span>
  </div>

  <div class="menu">
    <button onclick="showIsland()">Đảo kho báu</button>
    <button onclick="showShop()">Mua vật phẩm</button>
  </div>

  <div id="main"></div>

  <script>
    let diamonds = parseInt(localStorage.getItem('diamonds')) || 0;
    let digs = parseInt(localStorage.getItem('digs')) || 0;
    let currentTool = localStorage.getItem('currentTool') || 'xenggo';
    const toolStrength = { xenggo: 15, xengvang: 10, khoan: 5 };
    let currentDig = 0;

    function updateUI() {
      document.getElementById('diamonds').textContent = diamonds;
      document.getElementById('digs').textContent = digs;
      document.getElementById('item').textContent =
        currentTool === 'xenggo' ? 'Xẻng gỗ' :
        currentTool === 'xengvang' ? 'Xẻng vàng' : 'Máy khoan';

      localStorage.setItem('diamonds', diamonds);
      localStorage.setItem('digs', digs);
      localStorage.setItem('currentTool', currentTool);
    }

    function showIsland() {
      document.body.style.backgroundImage = "url('https://media.istockphoto.com/id/678719470/vi/anh/c%E1%BA%ADn-c%E1%BA%A3nh-m%C3%B4-h%C3%ACnh-c%C3%A1t-c%E1%BB%A7a-m%E1%BB%99t-b%C3%A3i-bi%E1%BB%83n-v%C3%A0o-m%C3%B9a-h%C3%A8.jpg?s=2048x2048&w=is&k=20&c=GkFzAsfrP5I2vIogPzGW_UHvWGMdl33Lw7KMXNU4-Qo=')";
      document.getElementById('main').innerHTML = `
        <img src="https://png.pngtree.com/png-clipart/20230913/original/pngtree-old-rusty-closed-treasure-chest-side-view-transparent-background-png-image_8864712.png" class="chest" onclick="digChest()">
        <p>Nhấn vào rương để đào!</p>
      `;
    }

    function showShop() {
      document.body.style.backgroundImage = "";
      document.getElementById('main').innerHTML = `
        <div class="shop-item">
          <h3>Xẻng vàng (20 💎)</h3>
          <img src="https://media.istockphoto.com/id/678719470/vi/anh/c%E1%BA%ADn-c%E1%BA%A3nh-m%C3%B4-h%C3%ACnh-c%C3%A1t-c%E1%BB%A7a-m%E1%BB%99t-b%C3%A3i-bi%E1%BB%83n-v%C3%A0o-m%C3%B9a-h%C3%A8.jpg?s=2048x2048&w=is&k=20&c=GkFzAsfrP5I2vIogPzGW_UHvWGMdl33Lw7KMXNU4-Qo=">
          <br><button onclick="buy('xengvang', 20)">Mua</button>
        </div>
        <div class="shop-item">
          <h3>Máy khoan (50 💎)</h3>
          <img src="https://bizweb.dktcdn.net/100/119/315/products/pixelcut-export-58-cc24b29a-58a0-4aa1-b484-4551e3c48afb.jpg?v=1736392501217">
          <br><button onclick="buy('khoan', 50)">Mua</button>
        </div>
      `;
    }

    function buy(tool, price) {
      if (diamonds >= price) {
        diamonds -= price;
        currentTool = tool;
        alert("Đã mua thành công!");
      } else {
        alert("Bạn không đủ kim cương!");
      }
      updateUI();
    }

    function digChest() {
      currentDig++;
      if (currentDig >= toolStrength[currentTool]) {
        let reward = Math.floor(Math.random() * 10) + 1;
        diamonds += reward;
        digs++;
        alert("Bạn đã mở rương và nhận " + reward + " kim cương!");
        currentDig = 0;
        updateUI();
      }
    }

    updateUI();
    showIsland();
  </script>

</body>
</html>
