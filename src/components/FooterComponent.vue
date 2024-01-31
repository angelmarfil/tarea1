<template>
      <footer class="footer">
    <a href="/" class="logo">
      <img src="http://www.utcancun.edu.mx/wp-content/uploads/2016/07/estetamano.png" alt="">
    </a>
    
    <div class="bottom">
  
      <div class="social">
        <a href="https://www.facebook.com/UTdeCancun" target="_blank">
          <i class="ri-facebook-circle-fill"></i>
        </a>
    
        <a href="https://www.instagram.com/utcancun/" target="_blank">
          <i class="ri-instagram-fill"></i>
        </a>
    
        <a href="https://twitter.com/UTCancun" target="_blank">
          <i class="ri-twitter-x-fill"></i>
        </a>
    
        <a href="https://www.youtube.com/UTCancun2012" target="_blank">
          <i class="ri-youtube-fill"></i>
        </a>
      </div>
  
      <small class="copyright">
        © 2024 Angel Marfil.
      </small>
    </div>

  </footer>
</template>

<style scoped>
.footer {
    margin-top: 3rem;
    background-color: oklch(0.51 0.12 169.4);
    color: var(--white-color);
    width: 100%;
    height: 300px;
    margin-top: 10vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
    

    & a {
        text-decoration: none;
        color: var(--white-color);
    }

    & .logo {
        width: 180px;
    }

    & .bottom {
        border-top: 2px solid var(--white-color);
        padding-top: 1rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        row-gap: 1rem;
    }

    & .social {
        display: flex;
        column-gap: 1.2rem;
        font-size: 1.4rem;
    }

    @media(width >= 768px){
        & .bottom {
            flex-direction: row-reverse;
            width: 90%;
            justify-content: space-between; 
        }
    }

}
</style>