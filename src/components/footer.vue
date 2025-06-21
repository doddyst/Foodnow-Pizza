<template>
  <footer class="footer">
    <div class="footer-container">
      
      <div class="footer-column">
        <img src="/logo-alt.svg" alt="Foodnow Logo" class="logo" />
        <div class="find-us">Find Us :</div>
        <div class="social-icons">
          <img src="/facebook.svg" alt="Facebook" />
          <img src="/instagram.svg" alt="Instagram" />
          <img src="/youtube.svg" alt="YouTube" />
        </div>
      </div>

      <div class="footer-column">
        <div class="column-title">Navigation</div>
        <div class="navigation-links">
          <div class="nav-left">
            <a href="#">Home</a>
            <a href="#">Order</a>
            <a href="#">About</a>
            <a href="#">Blog</a>
          </div>
          <div class="nav-right">
            <a href="#">Contact</a>
            <a href="#">Login</a>
            <a href="#">Register</a>
          </div>
        </div>
      </div>

      <div class="footer-column">
        <div class="column-title">Contact</div>
        <div class="contact-item">
          <img src="/mail.svg" alt="Mail" />
          Food.now@mail.com
        </div>
        <div class="contact-item">
          <img src="/phone.svg" alt="Phone" />
          +62848477102943
        </div>
        <div class="contact-item">
          <img src="/whatsapp.svg" alt="WhatsApp" />
          +628184938494
        </div>
      </div>

      <div class="footer-column">
        <div class="column-title">Location</div>
        <div class="location">
          <img src="/location.svg" alt="Location" />
          <div>
            <strong>Kerobokan</strong><br />
            Jl. Raya Kerobokan Br Taman, Kuta No.98,
            Kerobokan Kelod, Kec. Kuta Utara,
            Kabupaten Badung, Bali 80361
          </div>
        </div>
      </div>
    </div>

    <div class="footer-bottom">
      <p class="footer-text">
        © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor Indonesia. | Privacy Policy
      </p>
      <p>
        This site is protected by reCAPTCHA and the Google Privacy Policy and Terms of Service apply.
      </p>
    </div>
  </footer>
</template>



<style scoped lang="scss">
.footer {
  background-color: #F8F8F6;
  padding: 4rem 2rem 3rem;
  border-top: 1px solid #eee;
  font-family: 'Open Sans', sans-serif;
  color: #333;

  .footer-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 5rem;
    
    margin-left: 5rem;
    margin-right: 10rem;
    padding: 0 2rem;

    @media (max-width: 992px) {
      grid-template-columns: 1fr 1fr;
      gap: 3rem;
    }

    @media (max-width: 768px) {
      grid-template-columns: 1fr;
      text-align: center;
      padding: 0 1rem;
    }
  }

  .footer-column {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    align-items: flex-start;

    @media (max-width: 768px) {
      align-items: center;
    }

    .logo {
      width: 15rem;
      margin-bottom: 1.5rem;

      @media (max-width: 768px) {
        width: 10rem;
      }
    }

    .find-us,
    .column-title {
      font-size: 1.5rem;
      font-weight: 700;
      color: #e77e23;
    }

    .social-icons {
      display: flex;
      gap: 1.5rem;
      justify-content: flex-start;

      @media (max-width: 768px) {
        justify-content: center;
      }

      img {
        width: 2.8rem;
        height: 2.8rem;
        border: 1px solid #e77e23;
        border-radius: 50%;
        padding: 0.7rem;

        &:hover {
          background-color: #F8D8BD;
        }

        @media (max-width: 768px) {
          width: 2.25rem;
          height: 2.25rem;
          padding: 0.5rem;
        }
      }
    }

    .navigation-links {
      display: flex;
      gap: 4rem;

      .nav-left,
      .nav-right {
        display: flex;
        flex-direction: column;
        gap: 0.8rem;
      }

      @media (max-width: 768px) {
        flex-direction: column;
        align-items: center;
        gap: 1rem;
      }
    }

    a {
      text-decoration: none;
      color: #444;
      font-weight: 400;
      font-size: 1.1rem;

      &:hover,
      &.active {
        color: #e77e23;
        font-weight: 600;
      }

      @media (max-width: 768px) {
        font-size: 1rem;
      }
    }

    .contact-item,
    .location {
      display: flex;
      align-items: flex-start;
      gap: 0.75rem;
      font-size: 1.2rem;
      line-height: 1.6;

      img {
        width: 1.5rem;
        height: 1.5rem;
        margin-top: 0.2rem;
        flex-shrink: 0;
      }

      div {
        flex: 1;
        word-break: break-word;
      }

      @media (max-width: 768px) {
        justify-content: center;
        text-align: left;
        gap: 0.6rem;
      }
    }
  }

  .footer-bottom {
    border-top: 1px solid #eee;
    margin-top: 3rem;
    padding-top: 2rem;
    text-align: center;
    font-size: 1rem;

    .footer-text {
      margin-bottom: 1rem;
    }
  }
}

</style>
