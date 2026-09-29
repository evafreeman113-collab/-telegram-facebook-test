<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">

  <meta
    name="viewport"
    content="width=device-width, initial-scale=1.0, viewport-fit=cover"
  >

  <title>Telegram Mini App Test</title>

  <!-- Telegram Mini App SDK -->
  <script src="https://telegram.org/js/telegram-web-app.js"></script>

  <style>
    :root {
      --bg: var(--tg-theme-bg-color, #ffffff);
      --text: var(--tg-theme-text-color, #111111);
      --hint: var(--tg-theme-hint-color, #777777);
      --button: var(--tg-theme-button-color, #2481cc);
      --button-text: var(--tg-theme-button-text-color, #ffffff);
      --secondary: rgba(127, 127, 127, 0.15);
    }

    * {
      box-sizing: border-box;
    }

    html,
    body {
      margin: 0;
      padding: 0;
      min-height: 100%;
      background: var(--bg);
      color: var(--text);
      font-family:
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        Roboto,
        Arial,
        sans-serif;
    }

    body {
      min-height: 100vh;
      min-height: 100dvh;
      padding: 24px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .card {
      width: 100%;
      max-width: 520px;
      padding: 24px;
      border-radius: 20px;
      background: var(--secondary);
      text-align: center;
    }

    h1 {
      margin: 0 0 12px;
      font-size: 26px;
    }

    p {
      line-height: 1.5;
      color: var(--hint);
    }

    button {
      width: 100%;
      border: 0;
      border-radius: 12px;
      padding: 15px 18px;
      margin-top: 12px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      background: var(--button);
      color: var(--button-text);
    }

    button.secondary {
      background: transparent;
      color: var(--text);
      border: 1px solid rgba(127, 127, 127, 0.35);
    }

    #status {
      margin-top: 18px;
      font-size: 14px;
      color: var(--hint);
      word-break: break-word;
    }

    .info {
      margin-top: 20px;
      text-align: left;
      font-size: 13px;
      line-height: 1.6;
    }

    .info strong {
      color: var(--text);
    }
  </style>
</head>

<body>

  <main class="card">

    <h1>Telegram Mini App Test</h1>

    <p>
      This page tests whether the website is actually running
      inside Telegram's Mini App environment.
    </p>

    <button id="testButton">
      Test Telegram WebView
    </button>

    <button id="closeButton" class="secondary">
      Close Mini App
    </button>

    <div id="status">
      Initializing...
    </div>

    <div class="info">
      <div>
        <strong>Telegram:</strong>
        <span id="telegramStatus">Checking...</span>
      </div>

      <div>
        <strong>Platform:</strong>
        <span id="platform">Checking...</span>
      </div>

      <div>
        <strong>Version:</strong>
        <span id="version">Checking...</span>
      </div>
    </div>

  </main>

  <script>
    const tg = window.Telegram?.WebApp;

    const status = document.getElementById("status");
    const telegramStatus =
      document.getElementById("telegramStatus");
    const platform =
      document.getElementById("platform");
    const version =
      document.getElementById("version");

    const testButton =
      document.getElementById("testButton");

    const closeButton =
      document.getElementById("closeButton");


    // Check whether Telegram's Mini App API exists.
    if (tg) {

      tg.ready();
      tg.expand();

      telegramStatus.textContent = "YES";
      platform.textContent = tg.platform || "Unknown";
      version.textContent = tg.version || "Unknown";

      status.textContent =
        "Running inside Telegram Mini App.";

    } else {

      telegramStatus.textContent = "NO";
      platform.textContent = "Browser";
      version.textContent = "N/A";

      status.textContent =
        "This page is running in a normal browser.";

    }


    // Test button.
    testButton.addEventListener("click", function () {

      if (tg) {

        status.textContent =
          "SUCCESS: Telegram WebApp API is active.";

        tg.HapticFeedback?.impactOccurred("light");

      } else {

        status.textContent =
          "Telegram WebApp API was not detected.";

      }

    });


    // Close Mini App.
    closeButton.addEventListener("click", function () {

      if (tg && typeof tg.close === "function") {

        tg.close();

      } else {

        status.textContent =
          "There is no Telegram Mini App to close.";

      }

    });
  </script>

</body>
</html>