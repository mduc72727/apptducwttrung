<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trợ Năng Tduc </title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #111;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        .menu-container {
            width: 90%;
            max-width: 400px;
            margin: 20px auto;
            padding: 20px;
            border-radius: 15px;
            background: #222;
            box-shadow: 0px 0px 15px rgba(255, 0, 0, 0.8);
            border: 2px solid #ff0000;
        }
        .title {
            font-size: 22px;
            font-weight: bold;
            color: #ff0000;
            text-shadow: 0px 0px 10px rgba(255, 0, 0, 0.8);
            margin-bottom: 15px;
        }
        .toggle {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            margin: 10px 0;
        }
        .switch {
            position: relative;
            width: 45px;
            height: 22px;
        }
        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: gray;
            border-radius: 22px;
            transition: .4s;
        }
        .slider:before {
            position: absolute;
            content: "";
            height: 16px;
            width: 16px;
            left: 3px;
            bottom: 3px;
            background-color: white;
            border-radius: 50%;
            transition: .4s;
        }
        input:checked + .slider {
            background: linear-gradient(90deg, #ff0000, #ff6600);
            box-shadow: 0px 0px 10px rgba(255, 0, 0, 0.8);
        }
        input:checked + .slider:before {
            transform: translateX(22px);
        }
        select, input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: none;
            background: #333;
            color: white;
            text-align: center;
            font-size: 16px;
        }
        .slider-container {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-top: 10px;
        }
        input[type="range"] {
            flex-grow: 1;
            margin: 0 10px;
        }
        .confirm-btn, .open-game-btn {
            background: linear-gradient(90deg, #ff0000, #ff6600);
            color: white;
            padding: 12px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 5px;
            cursor: pointer;
            box-shadow: 0px 0px 10px rgba(255, 0, 0, 0.8);
            transition: 0.3s;
            margin-top: 15px;
            display: block;
            width: 100%;
        }
        .confirm-btn:hover, .open-game-btn:hover {
            background: linear-gradient(90deg, #ff6600, #ff0000);
        }
        .open-game-btn {
            display: none;
        }
    </style>
</head>
<body>
    <div class="menu-container">
        <div class="title">Tduc w Ttrung🫧</div>

        <div class="toggle">
            <span>UMP TRICK</span>
            <label class="switch">
                <input type="checkbox" id="ump_trick">
                <span class="slider"></span>
            </label>
        </div>

        <div class="toggle">
            <span>Aimlock</span>
            <label class="switch">
                <input type="checkbox" id="aimlock">
                <span class="slider"></span>
            </label>
        </div>

        <label>Chọn Vùng Aimlock:</label>
        <select id="aimlock_zone">
            <option value="head">Đầu</option>
            <option value="body">Ngực</option>
            <option value="legs">Chân</option>
        </select>

        <label>Tỷ lệ Headshot (%):</label>
        <div class="slider-container">
            <span id="headshot_value">50%</span>
            <input type="range" id="headshot_rate" min="0" max="100" value="50">
        </div>

        <label>Chọn DPI:</label>
        <input type="number" id="dpi" value="90">

        <label>Chọn Cấu Hình:</label>
        <select id="config">
            <option value="low">Thấp</option>
            <option value="medium">Vừa</option>
            <option value="high">Cao</option>
        </select>

        <div class="confirm-btn" onclick="saveSettingsAndOpenFFMax()">XÁC NHẬN</div>
        <div class="open-game-btn" id="openGameBtn" onclick="openFFMax()">MỞ FREE FIRE MAX</div>
    </div>

    <script>
        function saveSettingsAndOpenFFMax() {
            const settings = {
                ump_trick: document.getElementById("ump_trick").checked,
                aimlock: document.getElementById("aimlock").checked,
                aimlock_zone: document.getElementById("aimlock_zone").value,
                headshot_rate: document.getElementById("headshot_rate").value,
                dpi: document.getElementById("dpi").value,
                config: document.getElementById("config").value
            };
            localStorage.setItem("menuSettings", JSON.stringify(settings));

            if (!openFFMax()) {
                document.getElementById("openGameBtn").style.display = "block";
            }
        }

        function openFFMax() {
            let ffMaxURL = "ffmax://";
            window.location.href = ffMaxURL;

            setTimeout(() => {
                if (!document.hidden) {
                    alert("Không thể mở Free Fire MAX. Bấm vào nút MỞ GAME!");
                    return false;
                }
            }, 3000);
            return true;
        }

        document.getElementById("headshot_rate").oninput = function() {
            document.getElementById("headshot_value").innerText = this.value + "%";
        };
    </script>
</body>
</html>