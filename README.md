<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Parking</title>

    <style>
        body {
            font-family: Arial;
            background: #f4f4f4;
            text-align: center;
            padding: 20px;
            <h1>Sistem Smart Parking</h1>
            <p>Status Parking: <span id="parkingData">Loading...</span></p>

        }
        .lot {
            width: 120px;
            height: 120px;
            border-radius: 10px;
            margin: 15px;
            display: inline-block;
            font-size: 20px;
            color: black;
            line-height: 120px;
            font-weight: bold;
        }
        .empty { background: green; }
        .full { background: red; }
    </style>

    <!-- Firebase -->
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database.js"></script>


</head>
<body>

    <h2>SMART PARKING SYSTEM</h2>

    <div id="lot1" class="lot">Lot 1</div>
    <div id="lot2" class="lot">Lot 2</div>
    <div id="lot3" class="lot">Lot 3</div>
    <div id="lot4" class="lot">Lot 4</div>
    <div id="lot5" class="lot">Lot 5</div>

    <script>
      const firebaseConfig = {
        apiKey: "AIzaSyA_y99IxFHkfMjmeUg-VtIBX8tAwH7DlrE",
        authDomain: "smart-parking-aee.firebaseapp.com",
        databaseURL: "[https://YOUR_PROJECT.firebaseio.com](https://smart-parking-aee-default-rtdb.asia-southeast1.firebasedatabase.app)",
        projectId: "smart-parking-aee",
        storageBucket: "smart-parking-aee.firebasestorage.app",
        messagingSenderId: "85161961232",
        appId: "1:85161961232:web:a97b78b55b3e6728eda795"
      };

      // Initialize Firebase
      const app = firebase.initializeApp(firebaseConfig);
      const database = firebase.database();
    </script>
    
  database.ref("/parking/status").on("value", (snapshot) => {
    const status = snapshot.val();
    const display = document.getElementById("parkingData");

    if (status === 0) {
      display.innerText = "Kosong ✅";
      display.style.color = "green";
    } else {
      display.innerText = "Penuh ❌";
      display.style.color = "red";
    }
  });
</script>



        function updateLot(lotId, status) {
            const card = document.getElementById(lotId);
            if (status === 1) {
                card.classList.remove("empty");
                card.classList.add("full");
            } else {
                card.classList.remove("full");
                card.classList.add("empty");
            }
        }

        db.ref("parking/lot1").on("value", snap => updateLot("lot1", snap.val()));
        db.ref("parking/lot2").on("value", snap => updateLot("lot2", snap.val()));
        db.ref("parking/lot3").on("value", snap => updateLot("lot3", snap.val()));
        db.ref("parking/lot4").on("value", snap => updateLot("lot4", snap.val()));
        db.ref("parking/lot5").on("value", snap => updateLot("lot5", snap.val()));
    </script>

</body>
</html>
