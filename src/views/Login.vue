<template>
  <article class="login-view">
    <div class="login-view-inner container">
      <section class="login-inner">
        <h3>Login to Your Account</h3>
        <div class="login-with-social">
          <a href="#">
            <img
              src="/images/Authentications/GooglePlus.svg"
              alt="google-plus"
            />
          </a>
          <a href="#">
            <img
              src="/images/Authentications/Facebook.svg"
              alt="facebook"
            />
          </a>
          <a href="#">
            <img
              src="/images/Authentications/Linkedin.svg"
              alt="linkedin"
            />
          </a>
          <a href="#">
            <img src="/images/Authentications/Github.svg" alt="github" />
          </a>
        </div>
        <span>OR</span>
        <form class="login-form">
          <div class="input-group">
            <input type="email" id="login-email" placeholder="Email" />
            <img src="/images/Authentications/Email.svg" alt="email-icon" />
          </div>
          <div class="input-group">
            <input type="password" id="login-password" placeholder="Password" />
            <img
              src="/images/Authentications/Password.svg"
              alt="password-icon"
            />
          </div>

          <div class="input-group">
            <input type="checkbox" id="remember-me" />
            <label for="remember-me">Remember Me?</label>
            <router-link to="/reset">I forgot my password</router-link>
          </div>
          <button type="submit" class="submit-login-form-btn">SIGN IN</button>
        </form>
      </section>
      <section class="login-banner">
        <h3>New Here?</h3>
        <p>Signup and discover a great amount of new opportunities</p>
        <router-link to="/signup" class="signup-btn" type="button">
          SIGN UP
        </router-link>
        <div class="circle"></div>
      </section>
    </div>
  </article>
</template>
