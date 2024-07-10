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
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        .container {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            max-width: 600px;
            margin: 0 auto;
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
        .qr-code {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Travel and Hospitality Preferences</h1>
        <form id="preferencesForm">
            <div>
                <label for="transferFromDelhi">AC Bus Transfer from Delhi to Kashipur on 13 October</label>
                <select id="transferFromDelhi">
                    <option value="YES">YES</option>
                    <option value="NO">NO</option>
                </select>
            </div>
            <div>
                <label for="hotelTransfers">Hotel to IIM Campus and back to Hotel Transfers</label>
                <select id="hotelTransfers">
                    <option value="YES">YES</option>
                    <option value="NO">NO</option>
                </select>
            </div>
            <div>
                <label for="accommodation">Accommodation Preference</label>
                <select id="accommodation">
                    <option value="Single">Single</option>
                    <option value="Double">Double</option>
                    <option value="Triple">Triple</option>
                </select>
            </div>
            <div>
                <label for="transferToDelhi">AC Bus transfer from Kashipur to Delhi on 16 October</label>
                <select id="transferToDelhi">
                    <option value="YES">YES</option>
                    <option value="NO">NO</option>
                </select>
            </div>
            <p>Total Cost: <span id="totalCost">0</span> INR</p>
            <button type="button" onclick="calculateCost()">Calculate Cost</button>
            <button type="button" onclick="submitPreferences()">Done</button>
        </form>
        <div class="qr-code" id="qrCodeContainer"></div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrious/4.0.2/qrious.min.js"></script>
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
            const transferFromDelhi = document.getElementById('transferFromDelhi').value;
            const hotelTransfers = document.getElementById('hotelTransfers').value;
            const accommodation = document.getElementById('accommodation').value;
            const transferToDelhi = document.getElementById('transferToDelhi').value;

            const key = `${transferFromDelhi},${hotelTransfers},${accommodation},${transferToDelhi}`;
            const totalCost = costMatrix[key] || 0;
            document.getElementById('totalCost').textContent = totalCost;
        }

        function submitPreferences() {
            const transferFromDelhi = document.getElementById('transferFromDelhi').value;
            const hotelTransfers = document.getElementById('hotelTransfers').value;
            const accommodation = document.getElementById('accommodation').value;
            const transferToDelhi = document.getElementById('transferToDelhi').value;
            const totalCost = document.getElementById('totalCost').textContent;

            // Replace with your Google Forms endpoint
            const googleFormsEndpoint = '[https://docs.google.com/forms/d/e/1KljRZbBN48Y3tcbmHuIy0khzcMlkkFaXDl7RHeeX0Vw/formResponse](https://script.google.com/macros/s/AKfycbxKpAnecRugHybQaIpx2Uh6xBfHhdPuMeXbdWtCxCgNP723J9hZa7iPz5uluZmlOhmV/exec)';

            // Data to send to Google Forms
            const formData = new FormData();
            formData.append('entry.1234567890', transferFromDelhi);
            formData.append('entry.1234567891', hotelTransfers);
            formData.append('entry.1234567892', accommodation);
            formData.append('entry.1234567893', transferToDelhi);
            formData.append('entry.1234567894', totalCost);

            fetch(googleFormsEndpoint, {
                method: 'POST',
                body: formData,
                mode: 'no-cors'
            })
            .then(() => {
                alert('Preferences submitted successfully!');
                generateQRCode(totalCost);
            })
            .catch(error => console.error('Error submitting preferences:', error));
        }

        function generateQRCode(amount) {
            const qr = new QRious({
                element: document.getElementById('qrCodeContainer'),
                value: `upi://pay?pa=9993069529@pz&pn=Manish Choudhary&am=${amount}&cu=INR`,
                size: 200
            });
        }
    </script>
</body>
</html>
