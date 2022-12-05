<template>
  <article class="signup-view" id="signup">
    <div class="signup-view-inner container">
      <section class="signup-banner">
        <h3>Welcome Back!</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing</p>
        <router-link :to="{ name: 'login' }" class="login-btn" type="button">
          SIGN IN
        </router-link>
        <div class="circle"></div>
      </section>
      <section class="signup-inner">
        <h3>Create Account</h3>
        <div class="signup-with-social">
          <a href="#">
            <img
              src="/public/images/Authentications/GooglePlus.svg"
              alt="google-plus"
            />
          </a>
          <a href="#">
            <img
              src="/public/images/Authentications/Facebook.svg"
              alt="facebook"
            />
          </a>
          <a href="#">
            <img
              src="/public/images/Authentications/Linkedin.svg"
              alt="linkedin"
            />
          </a>
          <a href="#">
            <img src="/images/Authentications/Github.svg" alt="github" />
          </a>
        </div>
        <span>OR</span>
        <form class="signup-form">
          <div class="input-group">
            <input type="text" id="signup-username" placeholder="Username" />
            <img
              src="/public/images/Authentications/User.svg"
              alt="username-icon"
            />
          </div>
          <div class="input-group">
            <input type="email" id="signup-email" placeholder="Email" />
            <img src="/images/Authentications/Email.svg" alt="email-icon" />
          </div>
          <div class="input-group">
            <input
              type="password"
              id="signup-password"
              placeholder="Password"
            />
            <img
              src="/images/Authentications/Password.svg"
              alt="password-icon"
            />
          </div>

          <div class="input-group"></div>
          <button type="submit" class="submit-signup-form-btn">SIGN UP</button>
        </form>
      </section>
    </div>
  </article>
</template>
