<script setup>
import { RouterLink, RouterView } from 'vue-router';
import logo from '/src/assets/images/history-logo.png';

</script>

<template>
  <header>
      <nav class="nav">
        <img class="nav__logo" :src="logo" alt="logo" />
        <div class="nav__items">
          <RouterLink class="nav__items__item" to="/">Home</RouterLink>
          <RouterLink class="nav__items__item" to="/dinosaurs">Dinosaurs</RouterLink>
        </div>
      </nav>
  </header>

  <RouterView />
</template>

<style lang="scss" scoped>

.nav {
  position: absolute;
  top: 0;
  padding: 20px 42px;
  box-sizing: border-box;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: #fff;

  &__logo{
    width: 220px;
    height: auto;
    object-fit: cover;
  }

  &__items{

    &__item{
      color: #fff;
      text-decoration: none;

      &:not(:last-of-type){
        margin-right: 14px;
      }
    }
  }

}

</style>
