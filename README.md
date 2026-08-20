
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Wall-to-wall · vertical stack</title>
  <style>
    /* global reset – no margins, no padding, no scrollbars, no extra content */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      width: 100%;
      background: #000;  /* fallback, but images cover everything */
      overflow-x: hidden;
      overflow-y: auto;  /* allow scroll to see the full stack */
      scroll-behavior: smooth;
      font-size: 0;      /* kill inline whitespace */
      line-height: 0;
    }

    /* each image is a block that fills the entire viewport */
    .wall-image {
      display: block;
      width: 100vw;
      height: 100vh;          /* each image takes exactly one full screen */
      object-fit: cover;      /* wall‑to‑wall, no distortion, crops if needed */
      object-position: center;
      background: #000;       /* black behind image in case of loading */
      border: none;
      outline: none;
      margin: 0;
      padding: 0;
      vertical-align: top;    /* remove any extra spacing below image */
    }

    /* ensure no extra spacing from container */
    body {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: flex-start;
    }

    /* optional: smooth loading, but not required */
    .wall-image {
      transition: opacity 0.2s ease;
    }

    /* make sure images are never shrunk or stretched oddly */
    img {
      max-width: 100vw;
      max-height: 100vh;
    }

    /* override any browser default image spacing */
    img[src] {
      background: #000;
    }

    /* tiny accessibility: if images fail, show dark background */
    .wall-image:not([src]) {
      background: #111;
    }
  </style>
</head>
<body>
  <!-- 
    all pictures in exact order, one after another.
    each one is forced to be 100vw × 100vh – wall‑to‑wall.
    no text, no buttons, no overlays – just the images.
  -->
  <img class="wall-image" src="https://i.postimg.cc/D0Fs268D/Top-Banner.png" alt="Top Banner" />
  <img class="wall-image" src="https://i.postimg.cc/s2k7LsyY/Booking-Hours-Payments.png" alt="Booking Hours & Payments" />
  <img class="wall-image" src="https://i.postimg.cc/7ZQggSWC/Booking-Policies.png" alt="Booking Policies" />
  <!-- duplicate Booking Policies as requested (fourth image) -->
  <img class="wall-image" src="https://i.postimg.cc/7ZQggSWC/Booking-Policies.png" alt="Booking Policies (duplicate)" />
  <img class="wall-image" src="https://i.postimg.cc/tgKWcpyY/Important-Information.png" alt="Important Information" />
  <img class="wall-image" src="https://i.postimg.cc/xdwMZnYC/Selfies.png" alt="Selfies" />
  <img class="wall-image" src="https://i.postimg.cc/YS5YPMk0/Thank-You.png" alt="Thank You" />

  <!-- 
    no extra elements – exactly what you asked for.
    each image is full viewport width & height, stacked vertically.
    use the scrollbar to go down – wall‑to‑wall, no gaps.
  -->
</body>
</html>
