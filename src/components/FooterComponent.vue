<script></script>

<template>
  <footer>
    <div class="container-wrap">
      <div class="row">
        <div class="column">
          <div class="footer-widget about-widget">
            <h2 class="widget-title">About</h2>
            <p>sdjhfdsjfjsdkhfjkhsd</p>
          </div>
        </div>

        <div class="column">
          <div class="footer-widget categories-widget">
            <h2 class="widget-title">Categories</h2>
            <ul>
              <li><a href="#">Clothing</a></li>
              <li><a href="#">Lingerie</a></li>
              <li><a href="#">Babao</a></li>
              <li><a href="#">Marcelo</a></li>
              <li><a href="#">Jwellery</a></li>
              <li><a href="#">Jorlan</a></li>
            </ul>
          </div>
        </div>

        <div class="column">
          <div class="footer-widget information-widget">
            <h2 class="widget-title">Informations</h2>
            <ul>
              <li><a href="#">About us</a></li>
              <li><a href="#">Contact us</a></li>
              <li><a href="#">Term & Condition</a></li>
              <li><a href="#">Return & Exchange</a></li>
              <li><a href="#">Shipping & Delivery</a></li>
              <li><a href="#">Private Policy</a></li>
            </ul>
          </div>
        </div>

        <div class="column">
          <div class="footer-widget">
            <h2 class="widget-title">Contact</h2>
            <div class="contact-adress">
              <i class="fas fa-map-marker-alt"></i> Address: XYZ, New Delhi, India. Pin-Code: 17522272
            </div>
            <div class="contact-number">
              <i class="fas fa-phone-square-alt"></i> Phone: +14 996332930
            </div>
            <div class="contact-email">
              <i class="fas fa-envelope"></i> Email: contact@amazon.com
            </div>
            <div class="social-widget">
              <a href="#"><i class="fab fa-facebook-square"></i></a>
              <a href="#"><i class="fab fa-google-plus-square"></i></a>
              <a href="#"><i class="fab fa-instagram"></i></a>
              <a href="#"><i class="fab fa-youtube-square"></i></a>
              <a href="#"><i class="fab fa-twitter"></i></a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Parte inferior -->
    <div class="copyright-section">
      <p>Copyright @ 2025 All rights reserved</p>
      <div class="payment-info">
        <div class="cards">
          <i class="fab fa-cc-mastercard"></i>
          <i class="fab fa-cc-paypal"></i>
          <i class="fab fa-cc-amex"></i>
          <i class="fab fa-cc-visa"></i>
          <i class="fab fa-cc-discover"></i>
        </div>
        <p class="secure-text"><i class="fas fa-lock"></i> Secure Online Payment</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
footer {
  background-color: #ebe8e8;
  padding: 40px 20px 0 20px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.column {
  flex: 1;
  min-width: 220px;
  padding: 0 15px;
  margin-bottom: 30px;
}

.footer-widget {
  margin: 0;
  text-align: justify;
}

.widget-title {
  color: #000000;
  margin-bottom: 20px;
  text-transform: uppercase;
  font-size: 20px;
}

.about-widget p {
  line-height: 20px;
  margin: 10px 0 20px 0;
}

.footer-widget ul {
  list-style: none;
  padding-left: 0;
}

.footer-widget ul li {
  padding-bottom: 14px;
}

.footer-widget ul li a {
  color: #c2c0c0;
  text-decoration: none;
}

.footer-widget ul li a:hover {
  color: #000000;
  margin-left: 10px;
  transition: all 0.3s ease;
}

.contact-adress,
.contact-number,
.contact-email {
  margin: 10px 0;
  line-height: 1.5;
}

.contact-adress i,
.contact-number i,
.contact-email i {
  margin-right: 10px;
}

.social-widget a {
  font-size: 28px;
  color: #000000;
  margin-right: 10px;
}

.social-widget a:hover {
  color: #c2c0c0;
  transition: all 0.3s ease;
}


.copyright-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 2px solid #000;
  padding: 20px;
  margin-top: 30px;
}

.copyright-section p {
  color: #333;
  margin: 0;
}

.cards i {
  font-size: 26px;
  margin-right: 10px;
  color: #000;
}

.payment-info {
  text-align: right;
}

.secure-text {
  font-size: 14px;
  color: #555;
  margin-top: 5px;
}

@media (max-width: 768px) {
  .row {
    flex-direction: column;
    align-items: center;
  }

  .column {
    text-align: center;
  }

  .footer-widget ul {
    margin: 0 auto;
    padding: 0;
  }

  .copyright-section {
    flex-direction: column;
    text-align: center;
    gap: 10px;
  }

  .payment-info {
    text-align: center;
  }
}
</style>
