<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Creative Portfolio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #0e1015;
      --surface: #161922;
      --surface-hover: #1e2330;
      --text: #f3f4f6;
      --muted: #9ca3af;
      --accent: #9cad78; /* Sage-olive accent */
      --accent-soft: rgba(156, 173, 120, 0.16);
      --border: rgba(255, 255, 255, 0.08);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      font-family: "Inter", sans-serif;
      line-height: 1.6;
      overflow-x: hidden;
    }

    h1, h2, h3, .brand {
      font-family: "Space Grotesk", sans-serif;
    }

    /* Soft blurred cursor aura */
    #cursor-blob {
      position: fixed;
      top: 0;
      left: 0;
      width: 240px;
      height: 240px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(156, 173, 120, 0.22) 0%, rgba(156, 173, 120, 0) 70%);
      filter: blur(28px);
      pointer-events: none;
      transform: translate3d(-50%, -50%, 0);
      z-index: 0;
      opacity: 0;
      transition: opacity 0.4s ease;
    }

    /* Navigation */
    header {
      position: fixed;
      top: 0;
      width: 100%;
      z-index: 40;
      backdrop-filter: blur(12px);
