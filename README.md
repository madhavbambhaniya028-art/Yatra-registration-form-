# Yatra-registration-form-
Rajkot to haridwar 
<html>
<head>
  <title>Rajkot to Haridwar Yatra</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  
  <style>
    body {
      font-family: Arial;
      background: #f2f2f2;
      padding: 10px;
    }
    h2 { text-align: center; }
    input, select, button {
      width: 100%;
      padding: 10px;
      margin: 6px 0;
    }
    button {
      background: green;
      color: white;
      border: none;
      font-size: 16px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
      background: white;
    }
    table, th, td {
      border: 1px solid #000;
    }
    th, td {
      padding: 8px;
      text-align: center;
    }
  </style>
</head>

<body>

<h2>🚍 Rajkot to Haridwar Yatra Registration</h2>

<input id="name" placeholder="Full Name">
<input id="mobile" placeholder="Mobile Number">
<input id="address" placeholder="Address">
<select id="gender">
  <option value="">Select Gender</option>
  <option>Male</option>
  <option>Female</option>
</select>
<input type="date" id="date">

<button onclick="saveData()">Save Data</button>

<h2>📋 Yatri List</h2>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Mobile</th>
      <th>Address</th>
      <th>Gender</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody id="dataTable"></tbody>
</table>

<!-- Firebase -->
<script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>

<script>
  // 🔥 PASTE YOUR FIREBASE CONFIG HERE
  var firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT.firebaseio.com",
    projectId: "YOUR_PROJECT",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "XXXX",
    appId: "XXXX"
  };

  firebase.initializeApp(firebaseConfig);
  var database = firebase.database();

  function saveData() {
    var name = document.getElementById("name").value;
    var mobile = document.getElementById("mobile").value;
    var address = document.getElementById("address").value;
    var gender = document.getElementById("gender").value;
    var date = document.getElementById("date").value;

    if(name === "" || mobile === "") {
      alert("Name & Mobile required!");
      return;
    }

    database.ref("yatri").push({
      name, mobile, address, gender, date
    });

    alert("Data Saved Successfully ✅");
  }

  database.ref("yatri").on("value", function(snapshot) {
    var table = document.getElementById("dataTable");
    table.innerHTML = "";
    snapshot.forEach(function(child) {
      var d = child.val();
      table.innerHTML += `
        <tr>
          <td>${d.name}</td>
          <td>${d.mobile}</td>
          <td>${d.address}</td>
          <td>${d.gender}</td>
          <td>${d.date}</td>
        </tr>`;
    });
  });
</script>

</body>
</html>
