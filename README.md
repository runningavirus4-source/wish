<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Rainbow Cursor (Touch Friendly)</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: transparent;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: sans-serif;
    }
    h2 {
      color: #444;
      text-align: center;
    }
  </style>
</head>
<body>
  <h2>🌈 Touch or tap to see the rainbow effect!</h2>

  <!-- rainbow cursor library -->
  <script src="https://cdn.jsdelivr.net/gh/hi-imcodeman/rainbow-cursor/rainbow-cursor.js"></script>

  <script>
    // let the script react to finger movement
    document.addEventListener("touchmove", e => {
      if (!e.touches.length) return;
      const t = e.touches[0];
      const mouseMove = new MouseEvent("mousemove", {
        clientX: t.clientX,
        clientY: t.clientY
      });
      document.dispatchEvent(mouseMove);
    });

    // if no mouse or touch detected for a few seconds, move the rainbow automatically
    let autoDemo = true;
    document.addEventListener("mousemove", () => autoDemo = false);
    document.addEventListener("touchstart", () => autoDemo = false);

    let x = window.innerWidth / 2;
    let y = window.innerHeight / 2;
    function autoMove() {
      if (autoDemo) {
        x += Math.sin(Date.now() / 500) * 2;
        y += Math.cos(Date.now() / 500) * 2;
        document.dispatchEvent(new MouseEvent("mousemove", {clientX: x, clientY: y}));
      }
      requestAnimationFrame(autoMove);
    }
    autoMove();
  </script>
</body>
</html>
