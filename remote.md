---
layout: a_new_page
title: 'Available for Remote Work | Sudirman - Senior Software Developer'
permalink: /remote/
description: 'Senior Software Developer based in Indonesia (UTC+7). 17+ years building enterprise software — C#, SharePoint, CI/CD, E2E Testing, and always learning what comes next. Open to remote contracts and full-time roles worldwide.'
---

<style>
/* ── override minima theme ── */
body {
  background-color: #0f1117 !important;
}
.site-header {
  background-color: #0f1117 !important;
  border-top: none !important;
  border-bottom: 1px solid #2a2f3f !important;
}
.site-header .site-title,
.site-header .site-title:visited,
.site-nav .page-link {
  color: #e2e8f0 !important;
}
.site-footer {
  background-color: #0f1117 !important;
  border-top: 1px solid #2a2f3f !important;
  color: #7c8599 !important;
}
.site-footer a { color: #38bdf8 !important; }
.page-content {
  background-color: #0f1117 !important;
  padding-top: 1rem !important;
}
.post-header { display: none !important; }
.post-content h1,
.post-content h2,
.post-content h3 { color: #e2e8f0 !important; border: none !important; }
.wrapper { max-width: 900px !important; }

/* ── hire page ── */
.hire-wrap {
  font-family: 'Segoe UI', sans-serif;
  color: #e2e8f0;
  max-width: 820px;
  margin: 0 auto;
  padding: 0 0 4rem;
}

/* ── status badge ── */
.hire-badge {
  display: inline-flex;
  align-items: center;
  gap: .5rem;
  background: rgba(57,217,138,.1);
  border: 1px solid rgba(57,217,138,.3);
  border-radius: 100px;
  padding: .35rem 1rem;
  font-family: monospace;
  font-size: .78rem;
  color: #39d98a;
  margin-bottom: 1.6rem;
}
.hire-dot {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: #39d98a;
  animation: hire-pulse 2s infinite;
}
@keyframes hire-pulse {
  0%,100% { opacity:1; transform:scale(1); }
  50%      { opacity:.4; transform:scale(1.5); }
}

/* ── tagline ── */
.hire-tagline {
  font-size: 1rem;
  color: #7c8599;
  line-height: 1.75;
  margin-bottom: 1.5rem;
}
.hire-tagline strong { color: #e2e8f0; }

/* ── meta row ── */
.hire-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 2.5rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid #2a2f3f;
}
.hire-meta-item {
  font-family: monospace;
  font-size: .8rem;
  color: #7c8599;
}
.hire-meta-item strong { color: #e2e8f0; }
.hire-meta-item .hi   { color: #fbbf24; }

/* ── section title ── */
.hire-section-title {
  font-family: monospace;
  font-size: .7rem;
  letter-spacing: .12em;
  text-transform: uppercase;
  color: #38bdf8;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: .5rem;
}
.hire-section-title::before {
  content: '';
  display: inline-block;
  width: 18px; height: 1px;
  background: #38bdf8;
}

/* ── cards ── */
.hire-card {
  background: #181c27;
  border: 1px solid #2a2f3f;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1.2rem;
  transition: border-color .25s;
}
.hire-card:hover { border-color: rgba(56,189,248,.35); }

/* two-col grid */
.hire-grid-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.2rem;
}
@media (max-width: 600px) {
  .hire-grid-2 { grid-template-columns: 1fr; }
}

/* ── skill tags ── */
.hire-tags {
  display: flex;
  flex-wrap: wrap;
  gap: .55rem;
}
.hire-tag {
  font-family: monospace;
  font-size: .75rem;
  background: rgba(255,255,255,.05);
  border: 1px solid #2a2f3f;
  border-radius: 6px;
  padding: .28rem .7rem;
  color: #e2e8f0;
}
.hire-tag.hi {
  border-color: rgba(57,217,138,.4);
  color: #39d98a;
}

/* ── timeline ── */
.hire-timeline { display: flex; flex-direction: column; gap: .85rem; }
.hire-tl { display: flex; gap: .85rem; align-items: flex-start; }
.hire-tl-year {
  font-family: monospace;
  font-size: .72rem;
  color: #fbbf24;
  min-width: 38px;
  padding-top: 2px;
}
.hire-tl-text { font-size: .88rem; color: #7c8599; line-height: 1.55; }
.hire-tl-text strong { color: #e2e8f0; }

/* ── offer list ── */
.hire-offer-list { display: flex; flex-direction: column; gap: .8rem; }
.hire-offer { display: flex; gap: .75rem; align-items: flex-start; }
.hire-offer-dot {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: #39d98a;
  margin-top: 5px;
  flex-shrink: 0;
}
.hire-offer-text { font-size: .88rem; color: #7c8599; line-height: 1.5; }
.hire-offer-text strong { color: #e2e8f0; }

/* ── form ── */
.hire-form { display: flex; flex-direction: column; gap: .9rem; }
.hire-label {
  display: block;
  font-family: monospace;
  font-size: .7rem;
  letter-spacing: .08em;
  color: #7c8599;
  margin-bottom: .3rem;
}
.hire-input,
.hire-select,
.hire-textarea {
  width: 100%;
  background: rgba(255,255,255,.04);
  border: 1px solid #2a2f3f;
  border-radius: 8px;
  padding: .65rem .9rem;
  color: #e2e8f0;
  font-size: .9rem;
  outline: none;
  box-sizing: border-box;
  transition: border-color .2s, box-shadow .2s;
  font-family: 'Segoe UI', sans-serif;
}
.hire-input:focus,
.hire-select:focus,
.hire-textarea:focus {
  border-color: #38bdf8;
  box-shadow: 0 0 0 3px rgba(56,189,248,.1);
}
.hire-textarea { resize: vertical; min-height: 110px; }

.hire-btn {
  display: inline-flex;
  align-items: center;
  gap: .5rem;
  background: #39d98a;
  color: #0f1117;
  font-family: monospace;
  font-size: .85rem;
  font-weight: 700;
  border: none;
  border-radius: 8px;
  padding: .8rem 1.6rem;
  cursor: pointer;
  transition: opacity .2s, transform .15s;
}
.hire-btn:hover { opacity: .85; transform: translateY(-1px); }

#hire-confirm {
  display: none;
  background: rgba(57,217,138,.1);
  border: 1px solid rgba(57,217,138,.3);
  border-radius: 8px;
  padding: .9rem 1.1rem;
  font-family: monospace;
  font-size: .82rem;
  color: #39d98a;
}

/* ── footer note ── */
.hire-footer-note {
  text-align: center;
  font-family: monospace;
  font-size: .75rem;
  color: #7c8599;
  margin-top: 2rem;
}
.hire-footer-note a { color: #38bdf8; text-decoration: none; }

.post-content{margin-top: 100px !important;}
</style>

<div class="hire-wrap">

  <div class="hire-badge">
    <span class="hire-dot"></span>
    Available for Remote Work — 2026
  </div>

  <p class="hire-tagline">
    Build enterprise systems — SharePoint, C#, FrontEnd {Vue and an old AngularJS}, CI/CD, E2E Testing.<br/>
    Based in <strong>Indonesia (WIB, UTC+7)</strong>. Open to remote contracts and full-time roles worldwide.
  </p>

  <div class="hire-meta">
    <div class="hire-meta-item"><span class="hi">◎</span> <strong>Indonesia</strong> — UTC+7 / WIB</div>
    <div class="hire-meta-item"><span class="hi">◈</span> Remote · Contract · Full-time</div>
    <div class="hire-meta-item"><span class="hi">◇</span> English · Indonesian</div>
    <div class="hire-meta-item"><span class="hi">◉</span> <a href="https://softwaredeveloperx.com/workflow/" style="color:#38bdf8;text-decoration:none;">softwaredeveloperx.com/workflow</a></div>
  </div>

  <!-- Skills -->
  <div class="hire-card">
    <div class="hire-section-title">Core Skills</div>
    <div class="hire-tags">
      <span class="hire-tag hi">SharePoint Online</span>
      <span class="hire-tag hi">C# / .NET</span>
      <span class="hire-tag hi">SPFx</span>
	  <span class="hire-tag hi">FrontEnd {Vue and an old AngularJS}</span>
      <span class="hire-tag hi">E2E Testing</span>
      <span class="hire-tag hi">Document Driven Dev</span>
      <span class="hire-tag">SharePoint 2007 – 2016</span>
      <span class="hire-tag">Finite State Machine</span>
      <span class="hire-tag">CI / CD</span>
      <span class="hire-tag">GitHub Actions</span>
      <span class="hire-tag">REST API</span>
      <span class="hire-tag">IIS / Windows Server</span>
      <span class="hire-tag">SharePoint Migration</span>
      <span class="hire-tag">Multi-tenant Architecture</span>
      <span class="hire-tag">Technical Writing</span>
    </div>
  </div>

  <!-- Timeline + Offer side by side -->
  <div class="hire-grid-2">

    <div class="hire-card">
      <div class="hire-section-title">Journey</div>
      <div class="hire-timeline">
        <div class="hire-tl">
          <span class="hire-tl-year">2007</span>
          <div class="hire-tl-text"><strong>SharePoint WSS3 / MOSS</strong> — WebParts accessing SAP via ZBAPI</div>
        </div>
        <div class="hire-tl">
          <span class="hire-tl-year">2013</span>
          <div class="hire-tl-text"><strong>Livelink → SharePoint 2010</strong> — multi-country migration (ID, UK, VN, SG, CA)</div>
        </div>
        <div class="hire-tl">
          <span class="hire-tl-year">2017</span>
          <div class="hire-tl-text"><strong>SharePoint 2010 → 2013</strong> — DB-level migration</div>
        </div>
        <div class="hire-tl">
          <span class="hire-tl-year">2022</span>
          <div class="hire-tl-text"><strong>SharePoint 2013 → Online</strong> — cross-country team (ID, UK, VN, US)</div>
        </div>
        <div class="hire-tl">
          <span class="hire-tl-year">2023</span>
          <div class="hire-tl-text"><strong>SharePoint Online</strong> — solo-led migration project</div>
        </div>
        <div class="hire-tl">
          <span class="hire-tl-year">2024</span>
          <div class="hire-tl-text"><strong>Custom SPFx</strong> — fully branded SharePoint Online UI</div>
        </div>
        <div class="hire-tl">
          <span class="hire-tl-year">2025</span>
          <div class="hire-tl-text"><strong>C# system</strong> — DDD, FSM-based E2E testing, CI/CD multi-tenant</div>
        </div>
      </div>
    </div>

    <div class="hire-card">
      <div class="hire-section-title">What I Offer</div>
      <div class="hire-offer-list">
        <div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>SharePoint Consultant</strong> — migration, SPFx, SharePoint Online</div>
        </div>
        <div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>C# / .NET Developer</strong> — enterprise systems, APIs, data modelling</div>
        </div>
		<div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>Vue and an old AngularJS</strong> — FrontEnd web application</div>
        </div>
        <div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>Testing Architecture</strong> — E2E strategy, FSM scripts, generators</div>
        </div>
        <div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>CI/CD Setup</strong> — GitHub Actions, multi-tenant pipelines</div>
        </div>
        <div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>Technical Documentation</strong> — Document Driven Development, .MD file as Source of Truth</div>
        </div>
        <div class="hire-offer">
          <div class="hire-offer-dot"></div>
          <div class="hire-offer-text"><strong>Timezone:</strong> WIB (UTC+7) — overlaps well with AU, SG, MY, and EU mornings</div>
        </div>
      </div>
    </div>

  </div>

  <!-- Contact form -->
  <div class="hire-card">
    <div class="hire-section-title">Send a Message</div>
    <div class="hire-form">
      <div class="hire-grid-2">
        <div>
          <label class="hire-label">YOUR NAME</label>
          <input class="hire-input" type="text" id="hire-name" placeholder="Jane Smith" />
        </div>
        <div>
          <label class="hire-label">YOUR EMAIL</label>
          <input class="hire-input" type="email" id="hire-email" placeholder="jane@company.com" />
        </div>
      </div>
      <div>
        <label class="hire-label">TOPIC</label>
        <select class="hire-select" id="hire-topic">
          <option value="">— Select —</option>
          <option>SharePoint Migration / Consulting</option>
          <option>C# / .NET Development</option>
          <option>E2E Testing Architecture</option>
          <option>CI/CD Pipeline Setup</option>
          <option>Full-time Remote Role</option>
          <option>Other</option>
        </select>
      </div>
      <div>
        <label class="hire-label">YOUR MESSAGE</label>
        <textarea class="hire-textarea" id="hire-msg" placeholder="Tell me about your project or role..."></textarea>
      </div>
      <div>
        <button class="hire-btn" onclick="hireSend()">▶ Send Message</button>
      </div>
      <div id="hire-confirm">
        ✓ Thank you! I will get back to you soon.
      </div>
    </div>
  </div>

  <div class="hire-footer-note">
    Read my articles at
    <a href="https://softwaredeveloperx.com/workflow/">softwaredeveloperx.com/workflow</a>
    &nbsp;·&nbsp; Writing since 2023 &nbsp;·&nbsp; Sharing what I know
  </div>

</div>

<script>
function hireSend() {
  var name  = document.getElementById('hire-name').value.trim();
  var email = document.getElementById('hire-email').value.trim();
  var msg   = document.getElementById('hire-msg').value.trim();
  if (!name || !email || !msg) {
    alert('Please fill in Name, Email, and Message.');
    return;
  }
  /* 
    TO ACTIVATE: replace this block with a fetch() POST to Formspree.
    Example:
      fetch('https://formspree.io/f/YOUR_ID', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ name: name, email: email, message: msg })
      });
  */
  document.getElementById('hire-confirm').style.display = 'block';
}
</script>