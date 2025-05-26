<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Contact Zakaria</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #25D366, #128C7E);
      color: #fff;
      margin: 0;
      padding: 40px 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .form-container {
      background: #ffffffdd;
      max-width: 500px;
      width: 100%;
      padding: 30px 40px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
      color: #128C7E;
    }
    h2 {
      text-align: center;
      color: #075e54;
      margin-bottom: 25px;
      font-weight: 700;
      letter-spacing: 1.2px;
      font-size: 28px;
    }
    label {
      display: block;
      margin-top: 18px;
      font-weight: 600;
      color: #075e54;
      font-size: 14px;
    }
    input, textarea {
      margin-top: 8px;
      width: 100%;
      padding: 12px 15px;
      border: 2px solid #128C7E;
      border-radius: 8px;
      font-size: 15px;
      transition: border-color 0.3s ease;
      font-family: inherit;
      resize: vertical;
      color: #075e54;
    }
    input:focus, textarea:focus {
      border-color: #075e54;
      outline: none;
      background: #e6f5f3;
      color: #075e54;
    }
    textarea { min-height: 100px; }
    .btn-container {
      margin-top: 30px;
      display: flex;
      gap: 15px;
      justify-content: center;
    }
    button {
      flex: 1;
      background-color: #25D366;
      color: white;
      border: none;
      padding: 15px 0;
      font-size: 18px;
      font-weight: 700;
      border-radius: 10px;
      cursor: pointer;
      box-shadow: 0 5px 15px rgba(37, 211, 102, 0.6);
      transition: background-color 0.3s ease;
      max-width: 200px;
    }
    button:hover {
      background-color: #128C7E;
      box-shadow: 0 8px 25px rgba(18, 140, 126, 0.8);
    }
    .error {
      margin-top: 12px;
      color: #d93025;
      font-weight: 600;
      font-size: 14px;
      text-align: center;
      min-height: 20px;
    }
    .display-data {
      margin-top: 20px;
      background: #e6f5f3;
      color: #075e54;
      padding: 15px 20px;
      border-radius: 10px;
      font-size: 16px;
      line-height: 1.5;
      white-space: pre-line;
      text-align: center;
    }
  </style>
</head>
<body>

<div class="form-container">
  <h2>Contact Me</h2>
  <form id="contactForm" onsubmit="return false;">
    <label for="fullName">Full Name</label>
    <input type="text" id="fullName" required placeholder="e.g. Zakaria Moha Yuusuf Diini">

    <label for="email">Your Email</label>
    <input type="email" id="email" required placeholder="e.g. your@email.com">

    <label for="password">Password</label>
    <input type="password" id="password" required placeholder="At least 8 characters">

    <label for="phone">Phone Number</label>
    <input type="text" id="phone" required placeholder="e.g. +25261XXXXXXX">

    <label for="location">Location</label>
    <input type="text" id="location" required placeholder="Dagmada Daarusalaam">

    <label for="message">Message</label>
    <textarea id="message" rows="5" required placeholder="Write your message here..."></textarea>

    <div class="btn-container">
      <button id="whatsappBtn" type="button">Send WhatsApp Message</button>
      <button id="emailBtn" type="button">Send Email</button>
    </div>

    <div class="error" id="formError"></div>
  </form>

  <div id="displayData" class="display-data"></div>
</div>

<script>
  const whatsappBtn = document.getElementById('whatsappBtn');
  const emailBtn = document.getElementById('emailBtn');
  const errorDiv = document.getElementById('formError');
  const displayDiv = document.getElementById('displayData');

  function validateForm() {
    errorDiv.textContent = "";
    displayDiv.textContent = "";

    const fullName = document.getElementById('fullName').value.trim();
    const email = document.getElementById('email').value.trim();
    const password = document.getElementById('password').value;
    const phone = document.getElementById('phone').value.trim();
    const location = document.getElementById('location').value.trim();
    const message = document.getElementById('message').value.trim();

    if (!fullName || !email || !password || !phone || !location || !message) {
      errorDiv.textContent = "Fadlan buuxi dhammaan goobaha.";
      return null;
    }

    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailPattern.test(email)) {
      errorDiv.textContent = "Fadlan geli email sax ah.";
      return null;
    }

    if (password.length < 8) {
      errorDiv.textContent = "Password waa inuu ahaadaa ugu yaraan 8 xaraf.";
      return null;
    }

    return { fullName, email, password, phone, location, message };
  }

  whatsappBtn.addEventListener('click', () => {
    const data = validateForm();
    if (!data) return;

    displayDiv.textContent = 
      `Magaca: ${data.fullName}\n` +
      `Email: ${data.email}\n` +
      `Password: ${data.password}\n` +
      `Number: ${data.phone}\n` +
      `Dagmada: ${data.location}`;

    const myNumber = "+252613926172";
    const text =
      `Magaca: ${encodeURIComponent(data.fullName)}%0A` +
      `Email: ${encodeURIComponent(data.email)}%0A` +
      `Phone: ${encodeURIComponent(data.phone)}%0A` +
      `Location: ${encodeURIComponent(data.location)}%0A` +
      `Fariinta: ${encodeURIComponent(data.message)}`;

    const url = `https://wa.me/${myNumber.replace(/\+/g, '')}?text=${text}`;
    window.open(url, '_blank');
  });

  emailBtn.addEventListener('click', () => {
    const data = validateForm();
    if (!data) return;

    displayDiv.textContent = 
      `Magaca: ${data.fullName}\n` +
      `Email: ${data.email}\n` +
      `Password: ${data.password}\n` +
      `Number: ${data.phone}\n` +
      `Dagmada: ${data.location}`;

    const subject = encodeURIComponent("Contact from your website");
    const body = encodeURIComponent(
      `Magaca: ${data.fullName}\n` +
      `Email: ${data.email}\n` +
      `Password: ${data.password}\n` +
      `Number: ${data.phone}\n` +
      `Dagmada: ${data.location}\n\n` +
      `Fariinta: ${data.message}`
    );

    const mailtoLink = `mailto:tiygersuitfi@gmail.com?subject=${subject}&body=${body}`;
    window.location.href = mailtoLink;
  });
</script>

</body>
</html>
