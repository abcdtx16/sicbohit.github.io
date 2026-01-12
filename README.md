<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <title>sicbo hit.club</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
            margin: 0;
            padding: 20px;
        }

        h1 {
            text-align: center;
            color: #ff7a00;
            margin-bottom: 15px;
        }

        table {
            width: 100%;
            max-width: 600px;
            margin: 0 auto;
            border-collapse: collapse;
            background: #ffffff;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            border-radius: 10px;
            overflow: hidden;
        }

        th, td {
            padding: 10px;
            border-bottom: 1px solid #e0e0e0;
            text-align: center;
            font-size: 14px;
        }

        th {
            background: #fff3e6;
            font-weight: bold;
        }

        .loading {
            color: #999;
        }

        .predict {
            font-weight: bold;
            color: #dc3545;
        }

        .confidence {
            font-weight: bold;
            color: #198754;
        }
    </style>
</head>
<body>

<h1>789.CLUB</h1>

<table>
    <tr>
        <th>Phiên hiện tại</th>
        <td id="phien" class="loading">Đang tải...</td>
    </tr>
    <tr>
        <th>Dự đoán</th>
        <td id="duDoan" class="loading">Đang tải...</td>
    </tr>
    <tr>
        <th>Dự đoán vị</th>
        <td id="duDoanVi" class="loading">Đang tải...</td>
    </tr>
    <tr>
        <th>Độ tin cậy</th>
        <td id="doTinCay" class="loading">Đang tải...</td>
    </tr>
</table>

<script>
    async function loadData() {
        try {
            const res = await fetch("https://sichit-d15h.onrender.com/sicbo");
            const data = await res.json();

            const phien =
                data.phien_hien_tai || data.phien || data.session || "N/A";

            const duDoan =
                data.du_doan || data.predict || "N/A";

            const duDoanVi =
                data.du_doan_vi || data.predict_vi || data.vi || "N/A";

            const doTinCay =
                data.do_tin_cay || data.confidence || "N/A";

            document.getElementById("phien").innerText = phien;

            const duDoanEl = document.getElementById("duDoan");
            duDoanEl.innerText = duDoan;
            duDoanEl.className = "predict";

            document.getElementById("duDoanVi").innerText = duDoanVi;

            const doTinCayEl = document.getElementById("doTinCay");
            doTinCayEl.innerText = doTinCay;
            doTinCayEl.className = "confidence";

        } catch (e) {
            document.getElementById("phien").innerText = "Lỗi API";
            document.getElementById("duDoan").innerText = "Lỗi API";
            document.getElementById("duDoanVi").innerText = "Lỗi API";
            document.getElementById("doTinCay").innerText = "Lỗi API";
        }
    }

    loadData();
    setInterval(loadData, 5000);
</script>

</body>
</html>
