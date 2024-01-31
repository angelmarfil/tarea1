<script setup lang="ts">
    import { RouterLink } from "vue-router";
</script>

<template>
      <header class="header">
    <a href="/">
      <img src="../assets/logo.png" alt="" />
    </a>

    <nav>
      <menu>
        <li>
          <RouterLink to="/">
            <i class="ri-home-line"></i>
            Inicio
          </RouterLink>
        </li>
        <li>
          <RouterLink to="/about">
            <i class="ri-user-line"></i>
            Acerca de
          </RouterLink>
        </li>
      </menu>
    </nav>
  </header>
</template>

<style scoped>
    header {
  position: sticky;
  top: 0;
  z-index: 1;
  background-color: var(--white-color);
  height: 64px;
  padding: 0 16px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-shadow:
    rgba(17, 17, 26, 0.05) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 0px 8px;

  & img {
    height: 58px;
    width: 100%;
    object-fit: cover;
  }

  & menu {
    list-style: none;
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  & a {
    display: flex;
    align-items: center;
    column-gap: 0.5rem;
    justify-content: center;
    transition: background-color 0.3s;
    padding: 1.25rem 1.5rem;
    text-decoration: none;
    color: var(--black-color);
    font-size: 0.9rem;
  }
  
  & a:hover {
    background-color: rgba(17, 17, 26, 0.05);
  }

  & a i {
    font-size: 1.2rem;
    color: var(--black-color);
  }

}
</style>