# Aim Achiever Coaching Center

This is the official website of **Aim Achiever Coaching Center**.

<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aim Achiever Coaching Center</title>

  <style>
    body { font-family: Arial, sans-serif; background:#f5f5f5; margin:0; padding:0; }
    header { background:#1e88e5; color:white; padding:20px; text-align:center; }
    .container { padding:20px; max-width:900px; margin:auto; }
    h2 { color:#1e88e5; }
    form { background:white; padding:20px; border-radius:8px; box-shadow:0 0 10px rgba(0,0,0,0.1); }
    label { display:block; margin-top:10px; }
    input { width:100%; padding:8px; margin-top:5px; }
    button { margin-top:15px; padding:10px; width:100%; border:none; border-radius:5px; font-size:16px; cursor:pointer; }
    .pay { background:green; color:white; }
    .save { background:#1e88e5; color:white; }
    table { width:100%; border-collapse:collapse; margin-top:20px; background:white; }
    th, td { border:1px solid #ccc; padding:8px; text-align:center; }
    th { background:#e3f2fd; }
    footer { text-align:center; margin-top:20px; color:#555; }
  </style>
</head>

<body>

<header>
  <h1>Aim Achiever Coaching Center</h1>
  <p>Teachers: Zahid | Muzaffar | Ezaz</p>
  <p>Contact: 8172044264 , 9614541472 , 8967641559</p>
</header>

<div class="container">

  <h2>Student Admission Form</h2>

  <form id="studentForm">

    <label>Student Name</label>
    <input type="text" id="name" required>

    <label>Address (Ghar)</label>
    <input type="text" id="address" required>

    <label>Class</label>
    <input type="text" id="studentClass" required>

    <label>Fee (₹)</label>
    <input type="number" value="200" readonly>

    <!-- PhonePe Payment Button -->
    <a href="phonepe://pay?pa=8172044264@ybl&pn=Aim%20Achiever&am=200&cu=INR"
       onclick="paymentDone()">
      <button type="button" class="pay">Pay ₹200 via PhonePe</button>
    </a>

    <!-- Save Button -->
    <button type="submit" class="save">Payment Done & Save Student</button>

  </form>

  <h2>Admitted Students List</h2>

  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Address</th>
        <th>Class</th>
        <th>Fee (₹)</th>
      </tr>
    </thead>
    <tbody id="studentTable"></tbody>
  </table>

</div>

<footer>
  <p>© 2026 Aim Achiever Coaching Center</p>
</footer>

<script>
  const form = document.getElementById('studentForm');
  const table = document.getElementById('studentTable');
  let isPaid = false; // payment status

  function paymentDone() {
    isPaid = true;
    alert("✅ Payment button clicked\nAb student save kar sakte ho");
  }

  function loadStudents() {
    const students = JSON.parse(localStorage.getItem('students')) || [];
    table.innerHTML = "";
    students.forEach(s => {
      table.innerHTML += `
        <tr>
          <td>${s.name}</td>
          <td>${s.address}</td>
          <td>${s.className}</td>
          <td>200</td>
        </tr>`;
    });
  }

  form.addEventListener('submit', function(e) {
    e.preventDefault();

    if (!isPaid) {
      alert("❌ Pehle ₹200 PhonePe payment karo");
      return;
    }

    const student = {
      name: document.getElementById('name').value,
      address: document.getElementById('address').value,
      className: document.getElementById('studentClass').value
    };

    let students = JSON.parse(localStorage.getItem('students')) || [];
    students.push(student);
    localStorage.setItem('students', JSON.stringify(students));

    alert("✅ Payment ke baad student save ho gaya");
    form.reset();
    isPaid = false; // next student ke liye
    loadStudents();
  });

  loadStudents();
</script>

</body>
</html
