<script setup>
import Exit from "@/components/icons/exit.vue";
import MenuIcon from "@/components/icons/menu-icon.vue";
import {ref} from "vue";

const isOpen = ref(false)

</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header-wrapper">
        <ul class="header-list" :class="{open:isOpen}">
          <li><a href="#">Билеты и абонементы</a></li>
          <li><a href="#">Как купить?</a></li>
          <li><a href="#">Правила</a></li>
          <li><a href="#">Возврат билетов</a></li>
          <li>
            <a class="header-exit" href="#">
            <exit/>
            <div>Войти</div></a>
          </li>
        </ul>
        <div class="header-menu" @click="isOpen = !isOpen">
          <menu-icon/>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  padding: 2rem 0;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;

  &-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;
  }

  &-list {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex: 1 1 0;
    font-size: 1.5rem;

    li:first-child{
      text-transform: uppercase;
    }

    a{
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
  }

  &-exit {
    display: flex;
    gap: 0.5rem;
  }

  &-menu{
    z-index: 10;
    cursor: pointer;
  }
}

.container {
  padding: 0 2rem;
}

@media (max-width: 1200px) {
  .header{
    &-list{
      font-size: 1rem;
    }
  }
}

@media (max-width: 992px) {
  .header{
    &-wrapper{
      justify-content: end;
    }
    &-list{
      position: fixed;
      flex-direction: column;
      justify-content: center;
      padding: 5rem;
      gap: 2.5rem;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      transform: translateX(-100%);
      transition: all 0.3s ease;
      background: rgb(2,0,36);
      background: radial-gradient(circle, rgba(2,0,36,1) 0%, rgba(77,82,130,1) 0%, rgba(2,9,35,1) 71%);
      &::after{
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      border-radius: 50%;
      border: 2px solid white;
    }

    &::after {
      width: 65vw;
      height: 65vw;
    }

   
      &.open{
        transform: translateX(0);

      }
    }
  }
}

</style>