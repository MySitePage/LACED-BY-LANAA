<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
    <title>Wall-to-wall images · no extra content</title>
    <style>
        /* reset everything – no margins, no scrollbars, no extra elements */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            width: 100%;
            height: 100%;
            overflow: hidden;          /* kill scrollbars */
            background: #000;          /* fallback, but images cover everything */
        }

        /* the container fills the viewport exactly, no gaps */
        .wall {
            position: relative;
            width: 100vw;
            height: 100vh;
            background: #000;           /* visible only if images fail, but we want wall-to-wall */
            overflow: hidden;
        }

        /* each image is absolutely positioned, covers the whole screen, 
           and uses object-fit: cover to fill every pixel without distortion */
        .wall img {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;          /* ensures image fills the box, cropping if needed – wall-to-wall */
            display: block;
            transition: opacity 1.2s ease-in-out;
            opacity: 0;                /* hidden by default, only active image is visible */
            pointer-events: none;       /* no clicks, no interaction – just images */
            will-change: opacity;
        }

        /* the active image fades in */
        .wall img.active {
            opacity: 1;
            pointer-events: auto;       /* not needed but keeps consistency */
        }

        /* ensure images are never scaled down or warped – cover does that */
        /* optional: force hardware acceleration for smoother fades */
        .wall img {
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
        }

        /* tiny accessibility / noscript fallback – still wall-to-wall */
        .wall img:first-child {
            opacity: 1;                /* if js fails, first image shows (but we use js) */
        }

        /* remove any possible extra spacing from inline-block or whitespace */
        .wall {
            font-size: 0;
            line-height: 0;
        }
    </style>
</head>
<body>
    <div class="wall" id="wallContainer">
        <!-- all images in exact order as requested, each with full URL -->
        <img src="https://i.postimg.cc/D0Fs268D/Top-Banner.png" alt="Top Banner" class="active" />
        <img src="https://i.postimg.cc/s2k7LsyY/Booking-Hours-Payments.png" alt="Booking Hours Payments" />
        <img src="https://i.postimg.cc/7ZQggSWC/Booking-Policies.png" alt="Booking Policies" />
        <img src="https://i.postimg.cc/7ZQggSWC/Booking-Policies.png" alt="Booking Policies (duplicate)" />
        <img src="https://i.postimg.cc/tgKWcpyY/Important-Information.png" alt="Important Information" />
        <img src="https://i.postimg.cc/xdwMZnYC/Selfies.png" alt="Selfies" />
        <img src="https://i.postimg.cc/YS5YPMk0/Thank-You.png" alt="Thank You" />
    </div>

    <script>
        (function() {
            const container = document.getElementById('wallContainer');
            // get all image elements inside the container
            const images = container.querySelectorAll('img');
            if (!images.length) return;

            // start with first image active (already has class 'active' in markup)
            let currentIndex = 0;
            // store total count
            const total = images.length;

            // preload images? not strictly necessary, but helps with smooth transitions
            // we'll just let the browser handle it.

            // function to switch to a specific index
            function showImage(index) {
                // wrap around if index out of bounds
                if (index < 0) index = total - 1;
                if (index >= total) index = 0;

                // remove active class from all images
                for (let i = 0; i < total; i++) {
                    images[i].classList.remove('active');
                }
                // add active class to the target image
                images[index].classList.add('active');
                currentIndex = index;
            }

            // advance to next image, loop
            function nextImage() {
                let next = currentIndex + 1;
                if (next >= total) next = 0;
                showImage(next);
            }

            // start rotation: change every 3.5 seconds (feels natural, not too fast)
            let interval = setInterval(nextImage, 3500);

            // optional: pause on hover?  we keep it simple – no extra behavior.
            // but we want to keep it wall-to-wall with zero extra content.

            // if you want to ensure that images are fully loaded before starting,
            // but it's not needed – we start the interval immediately.
            // For robustness, if an image fails to load, it still transitions.

            // Also, we want to keep the first image visible if JS fails, 
            // but we have a fallback: the first img has 'active' class already.

            // For very old browsers that don't support object-fit: cover, 
            // we use background-image? No, we keep it simple with <img> + object-fit.
            // That's the cleanest wall-to-wall solution.

            // if the user resizes the window, images stay wall-to-wall because of CSS.

            // Edge case: if total images are less than 2, we don't need an interval,
            // but we have 7 images, so it's fine.

            // optional: we could add a small "pause" on interaction? 
            // but the instructions say: "don't add anything to it but these pictures" 
            // so we keep it minimal – no controls, no text, no dots, no extra elements.

            console.log('Wall-to-wall slideshow started – only images, no extra content.');
        })();
    </script>
</body>
</html>
