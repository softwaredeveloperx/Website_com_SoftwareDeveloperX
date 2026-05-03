---
layout: a_new_page
title: Contact
permalink: /contact/
---

<style>
.contact-content { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; }
.contact-form { background: #f8f9fa; padding: 40px; border-radius: 15px; }
.form-group { margin-bottom: 25px; }
.form-group label { display: block; margin-bottom: 8px; color: #2D1B4E; font-weight: 600; }
.form-group input,
.form-group select,
.form-group textarea {
  width: 100%; padding: 15px; border: 2px solid #ddd;
  border-radius: 8px; font-size: 1rem; transition: all 0.3s;
  font-family: Arial, sans-serif; background: white;
}
.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus { outline: none; border-color: #2D1B4E; }
.form-group textarea { min-height: 150px; resize: vertical; }
.submit-btn {
  background: linear-gradient(135deg, #2D1B4E 0%, #1a0f2e 100%);
  color: white; padding: 15px 40px; border: none; border-radius: 8px;
  font-size: 1.1rem; font-weight: 600; cursor: pointer; transition: all 0.3s;
}
.submit-btn:hover { transform: translateY(-2px); box-shadow: 0 10px 25px rgba(45,27,78,0.3); }
.contact-info h3 { font-size: 1.8rem; color: #2D1B4E; margin-bottom: 30px; }
.contact-item { margin-bottom: 25px; }
.contact-item h4 { color: #2D1B4E; margin-bottom: 8px; font-size: 1.1rem; }
.contact-item p { color: #666; font-size: 1rem; line-height: 1.7; }
@media (max-width: 768px) { .contact-content { grid-template-columns: 1fr; } }
</style>

<section class="content-section">
            <div class="container fade-in">
                <div class="section-header">
                  <h2>Get In Touch</h2>
                  <p>Let's discuss how we can help bring your vision to life</p>
                </div>

                <div class="contact-content">

  <div class="contact-form">
    <div class="form-group">
      <label>Your Name</label>
      <input type="text" placeholder="Your Name">
    </div>
    <div class="form-group">
      <label>Email Address</label>
      <input type="email" placeholder="Email Address">
    </div>
    <div class="form-group">
      <label>Phone Number</label>
      <input type="tel" placeholder="Phone Number">
    </div>
    <div class="form-group">
      <label>Service Needed</label>
      <select>
        <option value="">Service Needed</option>
        <option>Web Development</option>
        <option>Mobile App Development</option>
        <option>Custom Software</option>
        <option>Cloud Solutions</option>
        <option>API Development &amp; Integration</option>
        <option>IT Consulting</option>
      </select>
    </div>
    <div class="form-group">
      <label>Your Message</label>
      <textarea placeholder="Your Message"></textarea>
    </div>
    <button class="submit-btn" type="button">Send Message</button>
  </div>

  <div class="contact-info">
    <h3>Contact Information</h3>

    <div class="contact-item">
      <h4>📍 Address</h4>
      <p>Jl. Sudirman No. 123<br>Jakarta Selatan, 12190<br>Indonesia</p>
    </div>

    <div class="contact-item">
      <h4>📧 Email</h4>
      <p>hello@softwaredeveloperx.com<br>info@softwaredeveloperx.com</p>
    </div>

    <div class="contact-item">
      <h4>📱 Phone</h4>
      <p>+62 21 5555 1234<br>+62 812 3456 7890</p>
    </div>

    <div class="contact-item">
      <h4>🕒 Business Hours</h4>
      <p>Monday - Friday: 9:00 AM - 6:00 PM<br>Saturday: 10:00 AM - 3:00 PM<br>Sunday: Closed</p>
    </div>

    <div class="contact-item">
      <h4>Follow Us</h4>
      <p>GitHub: softwaredeveloperx<br>LinkedIn: SDR - Software DevelopeR</p>
    </div>

  </div>

</div>
            </div>
        </section>
