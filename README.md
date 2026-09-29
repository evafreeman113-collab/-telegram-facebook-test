<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Telegram Facebook Embed Test</title>

  <script src="https://telegram.org/js/telegram-web-app.js"></script>

  <style>
    * {
      box-sizing: border-box;
    }

    html,
    body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      background: #ffffff;
      font-family: Arial, sans-serif;
    }

    body {
      display: flex;
      flex-direction: column;
    }

    #top {
      padding: 12px;
      background: #1877f2;
      color: white;
      text-align: center;
    }

    #status {
      font-size: 13px;
      margin-top: 5px;
    }

    #facebook {
      width: 100%;
      flex: 1;
      border: 0;
      display: block;
    }
  </style>
</head>

<body>

  <div id="top">
    <strong>Facebook Embed Test</strong>
    <div id="status">Checking Telegram...</div>
  </div>

  <iframe
    id="facebook"
    src="https://www.facebook.com/"
    title="Facebook"
    allow="fullscreen">
  </iframe>

  <script>
    const status = document.getElementById("status");

    if (window.Telegram && window.Telegram.WebApp) {
      const tg = window.Telegram.WebApp;

      tg.ready();
      tg.expand();

      status.textContent =
        "Telegram Mini App detected — testing Facebook iframe...";
    } else {
      status.textContent =
        "Normal browser — Telegram Mini App not detected.";
    }
  </script>

</body>
</html>
