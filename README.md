<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Wall-to-wall · full screen images</title>
  <style>
    /* global reset – kill all margins, paddings, and extra spacing */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html, body {
      width: 100%;
      min-height: 100vh;
      background: #000;          /* fallback black, no white gaps */
      overflow-x: hidden;
      overflow-y: auto;          /* vertical scrolling to see all images */
      scroll-behavior: smooth;
      -webkit-tap-highlight-color: transparent;
      font-size: 0;             /* remove inline whitespace */
      line-height: 0;
    }

    /* the container holds all images and ensures no gaps */
    .wall {
      display: flex;
      flex-direction: column;
      width: 100vw;
      min-height: 100vh;
      background: #000;
    }

    /* each image: exactly full viewport width & height, wall-to-wall */
    .wall-image {
      display: block;
      width: 100vw;
      height: 100vh;            /* each takes one full screen */
      object-fit: cover;        /* cover the area, no distortion, no gaps */
      object-position: center;
      background: #000;         /* black behind image (if transparent) */
      border: none;
      outline: none;
      margin: 0;
      padding: 0;
      flex-shrink: 0;           /* prevent shrinking */
      flex-grow: 0;
      vertical-align: top;      /* kill any extra baseline space */
      -webkit-user-select: none;
      user-select: none;
      -webkit-touch-callout: none;
    }

    /* ensure no extra spacing from parent or children */
    .wall {
      font-size: 0;
      line-height: 0;
      letter-spacing: 0;
      word-spacing: 0;
    }

    /* for very tall screens or weird aspect ratios, keep images filling */
    @media (orientation: landscape) {
      .wall-image {
        width: 100vw;
        height: 100vh;
        object-fit: cover;
      }
    }

    /* mobile: still wall-to-wall, no gaps */
    @media (max-width: 480px) {
      .wall-image {
        width: 100vw;
        height: 100vh;
        object-fit: cover;
      }
    }

    /* safety: any extra spacing removed */
    img {
      display: block;
      max-width: 100vw;
      max-height: 100vh;
    }

    /* fallback if image fails to load – still black, no white */
    .wall-image:not([src]) {
      background: #111;
    }
    .wall-image[src=""] {
      background: #111;
    }

    /* remove any possible scrollbar gap on some browsers */
    ::-webkit-scrollbar {
      width: 0px;
      background: transparent;
    }
    /* but we keep scroll functionality, just hide the track if needed – but we want scroll visible? 
       actually we want users to scroll, so we keep default scrollbar but no gaps.
       we hide scrollbar only visually? we keep it for usability, but we don't add extra UI.
       we'll keep scrollbar visible so users know they can scroll down. */
  </style>
</head>
<body>
  <div class="wall">
    <!-- 
      all images in exact order, one after another.
      each forced to 100vw x 100vh – wall‑to‑wall, no gaps.
      no text, no buttons, no overlays – only pictures.
    -->
    <img class="wall-image" src="https://i.postimg.cc/D0Fs268D/Top-Banner.png" alt="Top Banner" loading="lazy" />
    <img class="wall-image" src="https://i.postimg.cc/s2k7LsyY/Booking-Hours-Payments.png" alt="Booking Hours & Payments" loading="lazy" />
    <img class="wall-image" src="https://i.postimg.cc/7ZQggSWC/Booking-Policies.png" alt="Booking Policies" loading="lazy" />
    <!-- duplicate Booking Policies as requested (fourth image) -->
    <img class="wall-image" src="https://i.postimg.cc/7ZQggSWC/Booking-Policies.png" alt="Booking Policies (duplicate)" loading="lazy" />
    <img class="wall-image" src="https://i.postimg.cc/tgKWcpyY/Important-Information.png" alt="Important Information" loading="lazy" />
    <img class="wall-image" src="https://i.postimg.cc/xdwMZnYC/Selfies.png" alt="Selfies" loading="lazy" />
    <img class="wall-image" src="https://i.postimg.cc/YS5YPMk0/Thank-You.png" alt="Thank You" loading="lazy" />
  </div>

  <!-- 
    absolutely no extra elements – exactly what you asked for.
    each image is full viewport width & height, stacked vertically.
    scroll down to see all images – wall‑to‑wall, zero gaps.
    works on mobile, tablet, desktop – responsive, wide, no white borders.
  -->
</body>
</html>
