# EaseIIMkashipur
Find comfort and convenience with KashiStay. Your ideal platform for booking accommodation and transfers for a memorable 3-day visit to IIM Kashipur, Uttarakhand
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Travel and Hospitality Preferences</title>
    <style>
        body {
            background-image: url('IIM.jpg');
            background-size: cover;
            background-position: center;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        .container {
            background-color: rgba(240, 240, 240, 0.9);
            padding: 20px;
            border-radius: 10px;
            max-width: 600px;
            margin: 0 auto;
            color: #000; /* Black text color */
        }
        input, select {
            margin: 10px 0;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            width: 100%;
            box-sizing: border-box;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #007bff;
            color: #fff;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .upi-id {
            margin-top: 20px;
            text-align: center;
        }
        .upi-id p {
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Travel and Hospitality Preferences</h1>
        <form id="preferencesForm">
            <div>
                <label>AC Bus Transfer from Delhi to Kashipur on 13 October</label>
                <select id="transferToKashipur">
                    <option value="YES">YES</option>
                    <option value="NO">NO</option>
                </select>
            </div>
            <div>
                <label>Hotel to IIM Campus and back to Hotel Transfers</label>
                <select id="hotelTransfers">
                    <option value="YES">YES</option>
                    <option value="NO">NO</option>
                </select>
            </div>
            <div>
                <label>Accommodation Preference</label>
                <select id="accommodation">
                    <option value="Single">Single</option>
                    <option value="Double">Double</option>
                    <option value="Triple">Triple</option>
                </select>
            </div>
            <div>
                <label>AC Bus transfer from Kashipur to Delhi on 16 October</label>
                <select id="transferToDelhi">
                    <option value="YES">YES</option>
                    <option value="NO">NO</option>
                </select>
            </div>
            <p>Total Cost: <span id="totalCost">0</span> INR</p>
            <button type="button" onclick="calculateCost()">Calculate Cost</button>
        </form>
        <div class="upi-id">
            <h3>Make Payment</h3>
            <p>UPI ID: 9993069529@pz</p>
        </div>
    </div>

    <script>
        const costMatrix = {
            'YES,YES,Single,YES': 11453,
            'YES,YES,Double,YES': 8453,
            'YES,YES,Single,NO': 9724,
            'YES,YES,Double,NO': 6724,
            'NO,YES,Single,YES': 9724,
            'NO,YES,Double,YES': 6724,
            'NO,YES,Single,NO': 7995,
            'NO,YES,Double,NO': 4995,
            'YES,YES,Triple,NO': 5725
        };

        function calculateCost() {
            const transferToKashipur = document.getElementById('transferToKashipur').value;
            const hotelTransfers = document.getElementById('hotelTransfers').value;
            const accommodation = document.getElementById('accommodation').value;
            const transferToDelhi = document.getElementById('transferToDelhi').value;

            const key = `${transferToKashipur},${hotelTransfers},${accommodation},${transferToDelhi}`;
            const totalCost = costMatrix[key] || 0;
            document.getElementById('totalCost').innerText = totalCost;
        }
    </script>
</body>
</html>
