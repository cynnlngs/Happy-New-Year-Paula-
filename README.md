<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Gift Reveal Version 2</title>
<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background: black;
  overflow: hidden;
  font-family: sans-serif;
}

/* COMMON SCREEN */
.screen {
  position: fixed;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.5s ease;
  z-index: 2;
}
.screen.show {
  opacity: 1;
  visibility: visible;
}

/* VIDEO */
#videoScreen video {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: pointer;
}

/* ENVELOPE */
.envelope-wrapper {
  position: relative;
  width: 200px;
  height: 130px;
  cursor: pointer;
  transform: scale(0);
  opacity: 0;
  transition: transform 0.8s ease, opacity 0.8s ease;
}
#envelopeScreen.show .envelope-wrapper {
  transform: scale(1);
  opacity: 1;
}
.picture {
  position: absolute;
  inset: 12px;
  background: white;
  overflow: hidden;
  z-index: 1;
}
.picture img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.back {
  position: absolute;
  inset: 0;
  background: #ead6b8;
  border-radius: 8px;
  z-index: 2;
}
.flap-wrapper {
  position: absolute;
  inset: 0;
  transform-origin: top;
  transition: transform 1s ease;
  z-index: 3;
}
.flap {
  position: absolute;
  inset: 0;
  background: #d8bb8c;
  clip-path: polygon(0 0, 100% 0, 50% 60%);
  z-index: 1;
}
.seal {
  position: absolute;
  width: 26px;
  height: 26px;
  background: #9e2a2b;
  border-radius: 50%;
  top: 48px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
}
.envelope-wrapper.open .flap-wrapper {
  transform: rotateX(180deg);
}

/* PICTURE 1 FULLSCREEN */
#picture1 img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  transition: transform 0.8s ease, opacity 0.8s ease;
}
</style>
</head>
<body>

<!-- VIDEO -->
<div id="videoScreen" class="screen show">
  <video autoplay muted loop>
    <source src="HNY2026.mp4" type="video/mp4">
  </video>
</div>

<!-- ENVELOPE -->
<div id="envelopeScreen" class="screen">
  <div class="envelope-wrapper" id="envelope">
    <div class="picture">
      <img src="HNY2026.jpg" alt="Envelope Picture">
    </div>
    <div class="back"></div>
    <div class="flap-wrapper">
      <div class="flap"></div>
      <div class="seal"></div>
    </div>
  </div>
</div>

<!-- PICTURE 1 FULLSCREEN -->
<div id="picture1" class="screen fullscreen">
  <img src="HNY2026.jpg" alt="Picture 1">
</div>

<script>
/* Step 1: Tap video → envelope */
document.getElementById("videoScreen").addEventListener("click", () => {
  document.getElementById("envelopeScreen").classList.add("show");
}, { once: true });

/* Step 2: Click envelope → show picture 1 */
document.getElementById("envelope").addEventListener("click", (e) => {
  e.stopPropagation();
  e.currentTarget.classList.add("open");
  setTimeout(() => {
    document.getElementById("envelopeScreen").classList.remove("show");
    document.getElementById("picture1").classList.add("show");
  }, 1200);
});
</script>
</body>
</html>
