<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Today Football Tips</title>
  <style>
    /* Reset */
    body, html {
      height: 100%;
      margin: 0;
      font-family: "Segoe UI", Arial, sans-serif;
    }

    /* Animated gradient background */
    body {
      background: linear-gradient(-45deg, #0b3d0b, #134d13, #1a601a, #0f440f);
      background-size: 400% 400%;
      animation: gradientFlow 15s ease infinite;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      text-align: center;
      color: #fff;
    }

    @keyframes gradientFlow {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .container {
      max-width: 480px;
      padding: 20px;
    }

    img {
      max-width: 220px;
      margin-bottom: 20px;
    }

    h1 {
      font-size: 30px;
      margin-bottom: 10px;
      font-weight: 600;
    }

    p {
      font-size: 17px;
      margin-bottom: 30px;
      color: #ddd;
    }

    a.button {
      display: inline-block;
      background: #ffcc00;
      color: #000;
      padding: 14px 36px;
      border-radius: 6px;
      text-decoration: none;
      font-weight: bold;
      font-size: 18px;
      box-shadow: 0 0 10px rgba(255, 204, 0, 0.7);
      animation: pulse 2s infinite;
      transition: 0.2s;
    }

    a.button:hover {
      background: #e6b800;
      box-shadow: 0 0 20px rgba(255, 204, 0, 1);
    }

    @keyframes pulse {
      0% {
        transform: scale(1);
        box-shadow: 0 0 10px rgba(255, 204, 0, 0.6);
      }
      50% {
        transform: scale(1.05);
        box-shadow: 0 0 20px rgba(255, 204, 0, 1);
      }
      100% {
        transform: scale(1);
        box-shadow: 0 0 10px rgba(255, 204, 0, 0.6);
      }
    }

    footer {
      margin-top: 40px;
      font-size: 13px;
      color: #aaa;
    }

    /* Mobile-first button */
    @media (max-width: 600px) {
      a.button {
        display: block;
        width: 100%;
        padding: 16px;
        font-size: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Replace with your uploaded GitHub image URL -->
    <img src="YOUR_IMAGE_URL_HERE" alt="Today Football Tips Logo">

    <h1>Today Football Tips</h1>
    <p>Get reliable football insights and updates daily.  
       Join our official Telegram channel below:</p>

    <a href="https://t.me/Todayfootball_tips" target="_blank" class="button">👉 Join Telegram</a>

    <footer>
      <p>© 2025 Today Football Tips. All rights reserved.<br>
      This page is for informational purposes only.</p>
    </footer>
  </div>
</body>
</html>
