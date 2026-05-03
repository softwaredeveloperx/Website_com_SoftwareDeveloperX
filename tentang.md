---
layout: a_new_page_id
title: Tentang
permalink: /tentang/
---

<style>

.about-content { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: center; margin-top: 20px; }
.about-text h3 { font-size: 2rem; color: #2D1B4E; margin-bottom: 20px; margin-top: 30px; }
.about-text h3:first-child { margin-top: 0; }
.about-text p { font-size: 1.1rem; line-height: 1.8; color: #555; margin-bottom: 20px; }
.about-image {
width: 100%; height: 500px;
background: linear-gradient(135deg, rgba(45,27,78,0.1), rgba(0,255,148,0.1));
border-radius: 20px; display: flex; align-items: center; justify-content: center;
}
@media (max-width: 768px) {
.about-content { grid-template-columns: 1fr; }
.about-image { height: 250px; }
}
</style>
<section class="content-section">
            <div class="container fade-in">
                <div class="section-header">
  <h2>About Us</h2>
  <p>Discover our journey and what drives us forward</p>
</div>

<div class="about-content">
  <div class="about-text">
    <h3>Who We Are</h3>
    <p>SDR adalah studio pengembangan software profesional yang berdedikasi untuk menciptakan solusi digital yang inovatif dan berkualitas tinggi. Dengan pengalaman bertahun-tahun dalam industri teknologi, kami telah membantu berbagai klien mewujudkan visi mereka menjadi kenyataan.</p>
    <p>Tim kami terdiri dari software developer berbakat, arsitek sistem, dan konsultan IT yang berpengalaman. Kami percaya bahwa software yang baik bukan hanya soal fungsionalitas, tetapi juga tentang memecahkan masalah nyata dan menciptakan pengalaman yang bermakna.</p>
    <h3>Our Mission</h3>
    <p>Misi kami adalah memberdayakan bisnis melalui teknologi yang powerful dan strategis. Kami berkomitmen untuk memberikan layanan terbaik dengan pendekatan yang personal dan hasil yang melampaui ekspektasi.</p>
  </div>
  <div class="about-image">
    <svg viewBox="0 0 200 200" width="200" height="200" xmlns="http://www.w3.org/2000/svg">
      <rect x="20" y="40" width="160" height="120" rx="10" fill="#2D1B4E"/>
      <rect x="35" y="60" width="130" height="80" rx="5" fill="#1a0f2e"/>
      <circle cx="100" cy="100" r="28" fill="#00FF94" opacity="0.85"/>
      <text x="100" y="107" text-anchor="middle" fill="#2D1B4E" font-size="18" font-weight="bold" font-family="Arial">SDR</text>
    </svg>
  </div>
</div>
            </div>
        </section>
