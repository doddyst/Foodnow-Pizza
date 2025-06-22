<template>
  <div class="header">
    <header class="navbar">
      <div class="logo">
        <img src="/logo.svg" alt="logo" />
      </div>

      <nav class="nav-links" :class="{ open: menuOpen }">
        <a href="#">Home</a>
        <a href="#" class="active">Order</a>
        <a href="#">About</a>
        <a href="#">Blog</a>
        <a href="#">Contact us</a>
      </nav>

      <div class="auth-buttons" :class="{ open: menuOpen }">
        <a href="#" class="login">Login</a>
        <a href="#" class="register">Register</a>
      </div>

      <div class="hamburger" @click="menuOpen = !menuOpen">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </header>

    <div class="header-content">
      <h1>Pizza order</h1>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const menuOpen = ref(false)
</script>



<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap');

.header {
  position: relative;
  width: 100%;
  height: 46.1rem;
  background: url('/hero.png') center center / cover no-repeat;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  overflow: hidden;
}

.navbar {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  height: 6.3rem;
  padding: 1.5rem 4rem;
  display: flex;
  justify-content: space-between;
  align-items: center;

  .logo {
    display: flex;
    align-items: center;
    margin-top: 0.6rem;
    margin-left: 3.6rem;

    img {
      height: 2.5rem;
      width: 13.4rem;
      margin-left: 1rem;
    }
  }

  .nav-links,
  .auth-buttons {
    display: flex;
    align-items: center;
    gap: 1.9rem;

    a {
      font-size: 1.1rem;
      font-weight: 630;
      color: white;
      text-decoration: none;

      &:hover {
        color: #E77E23;
      }

      &.active {
        color: #E77E23;
        font-weight: 600;
      }
    }
  }

  .auth-buttons {
    margin-right: 4.1rem;

    .register {
      background-color: #E77E23;
      color: white;
      font-weight: 600;
      padding: 0.8rem 2.6rem;
      font-size: 1.1rem;
      border-radius: 999px;
      text-decoration: none;

      &:hover {
        background-color: #C16515;
        color: white;
      }
    }
  }

  .hamburger {
    display: none;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 0.5rem;
    gap: 0.4rem;
    cursor: pointer;

    span {
      width: 2rem;
      height: 0.25rem;
      background: white;
      border-radius: 5px;
    }

    @media (max-width: 992px) {
      display: flex;
    }
  }
}

.header-content {
  position: relative;
  z-index: 1;
  margin-top: 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

  h1 {
    font-size: 6rem;
    font-weight: 700;
    line-height: 1.1;
    color: #E77E23;
  }
}

/* Tablet Style (768px–992px) */
@media (max-width: 992px) {
  .navbar {
    flex-direction: column;
    align-items: center;
    padding: 1.5rem 2rem;

    .logo {
      margin: 0;
    }

    .nav-links,
    .auth-buttons {
      display: none;
      flex-direction: column;
      align-items: center;
      width: 100%;
      margin-top: 1rem;
      gap: 1rem;
    }

    .nav-links.open,
    .auth-buttons.open {
      display: flex;
    }

    .nav-links a,
    .auth-buttons a {
      color: white;
      font-size: 1rem;
      font-weight: 400;
      text-decoration: none;
      text-align: center;

      &:hover {
        color: #E77E23;
      }

      &.active {
        color: white;
        font-weight: 400;
      }
    }

    .auth-buttons {
      margin-right: 0 !important;
      text-align: center;

      .register {
        background: none;
        padding: 0;
        border-radius: 0;
        font-weight: 400;

        &:hover {
          color: #E77E23;
          background: none;
        }
      }
    }
  }

  .header-content {
    margin-top: 26rem;

    h1 {
      font-size: 3rem;
      text-align: center;
    }
  }
}
</style>
