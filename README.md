<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đảo Kho Báu</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
        }
        #treasureIsland {
            background-image: url('https://www.istockphoto.com/vi/anh/c%E1%BA%ADn-c%E1%BA%A3nh-m%C3%B4-h%C3%ACnh-c%C3%A1t-c%E1%BB%A7a-m%E1%BB%99t-b%C3%A3i-bi%E1%BB%83n-v%C3%A0o-m%C3%B9a-h%C3%A8-gm678719470-125832651');
            background-size: cover;
            height: 500px;
            text-align: center;
            padding-top: 100px;
            color: white;
        }
        #shopSection {
            text-align: center;
            margin-top: 30px;
        }
        .item {
            margin: 20px;
            display: inline-block;
            background-color: #fff;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .item img {
            width: 100px;
            height: 100px;
        }
        .item button {
            padding: 10px;
            margin-top: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .item button:disabled {
            background-color: #ccc;
        }
        .status {
            margin-top: 20px;
            font-size: 18px;
        }
        .inventory {
            margin-top: 30px;
        }
    </style>
</head>
<body>

    <div id="treasureIsland">
        <h1>Chào mừng đến Đảo Kho Báu</h1>
        <p>Số kim cương: <span id="diamonds">0</span> 💎</p>
        <p>Số lần đào: <span id="digCount">0</span></p>
        <p>Vật dụng: <span id="currentItem">Xẻng gỗ</span></p>
        <button onclick="digForTreasure()">Đào kho báu</button>
    </div>

    <div id="shopSection">
        <h2>Mua vật phẩm</h2>
        
        <div class="item">
            <img src="https://www.vecteezy.com/free-png/30926533-3d-shovel-illustration" alt="Xẻng vàng">
            <p>Xẻng vàng (20 💎)</p>
            <button id="buyGoldShovel" onclick="buyItem('goldShovel')" disabled>Chưa mua</button>
        </div>

        <div class="item">
            <img src="https://www.vecteezy.com/free-png/30926533-3d-shovel-illustration" alt="Máy khoan">
            <p>Máy khoan (50 💎)</p>
            <button id="buyDrill" onclick="buyItem('drill')" disabled>Chưa mua</button>
        </div>
    </div>

    <div id="inventorySection">
        <h2>Kho Vật Dụng</h2>
        <div class="inventory">
            <p><strong>Vật dụng hiện tại: </strong><span id="inventoryItem">Xẻng gỗ</span></p>
            <p><strong>Số lần đào cần thiết: </strong><span id="digRequired">15</span></p>
        </div>
    </div>

    <div class="status">
        <p id="statusMessage"></p>
    </div>

    <script>
        let diamonds = 0;
        let digCount = 0;
        let currentItem = 'woodenShovel';
        let digRequired = 15;

        function updateStatus(message) {
            document.getElementById('statusMessage').innerText = message;
        }

        function updateDiamonds(amount) {
            diamonds += amount;
            document.getElementById('diamonds').innerText = diamonds;
        }

        function updateDigCount() {
            digCount++;
            document.getElementById('digCount').innerText = digCount;
        }

        function updateItem(newItem, newDigRequired) {
            currentItem = newItem;
            digRequired = newDigRequired;
            document.getElementById('currentItem').innerText = newItem === 'goldShovel' ? 'Xẻng vàng' : (newItem === 'drill' ? 'Máy khoan' : 'Xẻng gỗ');
            document.getElementById('inventoryItem').innerText = newItem === 'goldShovel' ? 'Xẻng vàng' : (newItem === 'drill' ? 'Máy khoan' : 'Xẻng gỗ');
            document.getElementById('digRequired').innerText = newDigRequired;
        }

        function digForTreasure() {
            if (digCount < digRequired) {
                updateStatus(`Còn ${digRequired - digCount} lần nữa để mở rương.`);
            } else {
                let diamondsFound = Math.floor(Math.random() * 10) + 1;
                updateDiamonds(diamondsFound);
                updateDigCount();
                updateStatus(`Mở rương thành công! Bạn nhận được ${diamondsFound} 💎.`);
                digCount = 0;
            }
        }

        function buyItem(item) {
            if (item === 'goldShovel' && diamonds >= 20) {
                updateDiamonds(-20);
                updateItem('goldShovel', 10);
                document.getElementById('buyGoldShovel').innerText = 'Đã mua';
                document.getElementById('buyGoldShovel').disabled = true;
            } else if (item === 'drill' && diamonds >= 50) {
                updateDiamonds(-50);
                updateItem('drill', 5);
                document.getElementById('buyDrill').innerText = 'Đã mua';
                document.getElementById('buyDrill').disabled = true;
            } else {
                updateStatus('Không đủ kim cương để mua!');
            }
        }

        function enableButtons() {
            if (diamonds >= 20 && !document.getElementById('buyGoldShovel').disabled) {
                document.getElementById('buyGoldShovel').disabled = false;
            }
            if (diamonds >= 50 && !document.getElementById('buyDrill').disabled) {
                document.getElementById('buyDrill').disabled = false;
            }
        }

        setInterval(enableButtons, 1000); // Kiểm tra mỗi giây để bật nút mua khi đủ kim cương
    </script>

</body>
</html>
