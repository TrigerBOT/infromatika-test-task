<script setup>
import {Swiper, SwiperSlide} from 'swiper/vue';
import {Mousewheel} from "swiper/modules";
import Header from "@/components/Header.vue";
import 'swiper/css';
import {ref} from 'vue'

let swiperInstance = ref(null)
const events = [
  {
    id: 1,
    place: 'Кухня ресторана',
    date: '30 мая',
    time: '17:00',
    teamHome: 'ШЕФ',
    teamGuest: 'Огузок',
    link: 'https://www.youtube.com/watch?v=Xz0DjqPSbyc'
  },
  {
    id: 2,
    place: 'Клуб',
    date: '17 июня',
    time: '17:00',
    teamHome: 'Тимати',
    teamGuest: 'Dj Dlee',
    link: 'https://www.youtube.com/watch?v=jYqsEj9MKS4'
  },
  {
    id: 3,
    place: 'Стадион',
    date: '26 июня',
    time: '17:00',
    teamHome: 'Team Spirit',
    teamGuest: 'BetBoom',
    link: 'https://www.youtube.com/watch?v=iMqMtv6sD6M'
  },
  {
    id: 4,
    place: 'Стадион',
    date: '16 июля',
    time: '17:00',
    teamHome: 'Локомотив',
    teamGuest: 'Тамбов',
    link: 'https://www.youtube.com/watch?v=NOaKPbkJg-I'
  },
  {
    id: 5,
    place: 'Скамейка у подъезда',
    date: '30 сентября',
    time: '17:00',
    teamHome: 'Айфоны',
    teamGuest: 'Андроеды',
    link: 'https://www.youtube.com/watch?v=9WRktF1cNgc'
  },
]
let teamHome = ref(null);
let teamGuest = ref(null);
const onSwiper = (swiper) => {
  swiperInstance = swiper
};

const onSlideChange = (e) => {
  teamHome.value = events.find(x => x.id === e.activeIndex + 1).teamHome
  teamGuest.value = events.find(x => x.id === e.activeIndex + 1).teamGuest
};
const slideEventsTo = (position) => {
  swiperInstance?.slideTo(position - 1)
}

const modules = [Mousewheel]

</script>

<template>
  <Header/>
  <main>
    <div class="events-wrapper">
      <swiper
          :slides-per-view="3"
          :modules="modules"
          :centeredSlides="true"
          :initial-slide="2"
          :watchSlidesProgress="true"
          :mousewheel="true"
          :speed="300"
          :breakpoints="{992:{ slidesPerView:5, } }"
          @swiper="onSwiper"
          @slideChange="onSlideChange"
      >
        <swiper-slide
            @click="slideEventsTo(event.id)"
            v-slot="{ isVisible }"
            v-for="event in events">
          <div class="events-item" :class="{notVisible: !isVisible}">
            <div class="events-item__place">{{ event.place }}</div>
            <div class="events-item__date">{{ event.date }}</div>
            <div class="events-item__time">{{ event.time }}</div>
            <a class="events-item__link" :href="event.link" target="_blank">Купить</a>
          </div>
        </swiper-slide>
      </swiper>
      <div class="team team-home">
        {{ teamHome }}
      </div>
      <div class="team team-guest">
        {{ teamGuest }}
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
.team {
  position: absolute;
  z-index: 10;
  width: 310px;
  font-size: 3rem;
  white-space: nowrap;
  color: black;

  &-home, &-guest{
    &:before{
      content: "";
      position: absolute;
      width: 1000px;
      height: 150px;
      -webkit-transform: skew(-30deg);
      -moz-transform: skew(-30deg);
      -o-transform: skew(-30deg);
      transform:skew(-30deg);
      background: white;
      border-radius: 15px;
      z-index: -2;
    }
  }

  &-home {
    top: 50%;
    left: 50%;
    transform: translate(-165%, -210%);

    &:before {
      top: -40px;
      right: -40px;
    }
  }

  &-guest {
    bottom: 50%;
    right: 50%;
    transform: translate(165%, 185%);

    &:before {
      top: -40px;
      left: -40px;
    }
  }
}

.events {
  &-wrapper {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;

    &:before, &:after{
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      border-radius: 50%;
      border: 2px solid white;
    }

    &:before {
      width: 35vw;
      height: 35vw;
    }

    &:after {
      width: 60vw;
      height: 60vw;
    }
  }

  &-item {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: white;
    color: black;
    cursor: pointer;
    position: relative;
    top: 0;
    margin: 0 auto;
    width: 4em;
    height: 6.52em;
    border-radius: 6px;
    transition: all .6s ease;
    align-items: center;
    text-align: center;

    &:before, &:after {
      position: absolute;
      width: inherit;
      height: inherit;
      border-radius: inherit;
      background: inherit;
      content: "";
      z-index: -1;
    }

    &:before {
      position: absolute;
      top: 0;
      transform: rotate(60deg);
    }

    &:after {
      position: absolute;
      top: 0;
      transform: rotate(-60deg);
    }

    &__date {
      font-weight: 600;
      white-space: nowrap;
      text-transform: uppercase;
      font-size: 14px;
      word-wrap: break-word;
    }

    &__place, &__time, &__link {
      transition: all 0.3s ease;
      display: none;

    }
    &__place{
      font-size: 12px;
    }
    &__link {
      padding: 0.25rem 0.5rem;
      border-radius: 0.25rem;
      border: 1px solid black;

      &:hover {
       box-shadow: 2px 2px black;
      }
    }
  }
}

.notVisible {
  display: none;
}

.swiper {
  width: 80%;
  height: 100%;

  &-slide {
    display: flex;
    align-items: center;
    justify-content: end;

    .events-item {
      margin-right: 0;
      transition: all 1.5s ease;
      transform: translateY(250%);
    }

    &-active {
      .events-item {
        margin: 0 auto;
        transform: translateY(0) scale(3);
      }

      .events-item__place, .events-item__time, .events-item__link {
        transform: scale(0.75);
        display: block;
      }
    }

    &-prev {
      .events-item {
        margin: 0 auto;
        transform: translateY(150%) scale(1.5);
      }
    }

    &-next {
      .events-item {
        margin: 0 auto;
        transform: translateY(-150%) scale(1.5);
      }

      & + .swiper-slide {
        .events-item {
          margin-left: 0;
          margin-right: auto;
          transform: translateY(-250%);
        }
      }
    }
  }
}

@media (max-width:1400px) {
  .swiper{
    width: 100%;
  }
}

@media (max-width: 1200px) {
  .team {
    font-size: 2.5rem;
    &-home, &-guest{
      &:before{
        height: 120px;
      }
    }

    &-home {
      text-align: end;
    }

    &-guest {
      transform: translate(165%, 210%);
    }

  }

  .swiper {
    &-slide {
      &-active {
        .events-item {
          transform: scale(2.5);
        }
      }
    }
  }
}

@media (max-width: 992px) {
  .swiper{
    width: 80%;
  }
  .team {
    font-size: 1.5rem;
    &-home, &-guest{
      &:before{
        height: 100px;
      }
    }

    &-home {
      text-align: end;
      transform: translate(-155%, -320%);
    }

    &-guest {
      transform: translate(154%, 350%);
    }
  }


}

@media (max-width: 768px) {
  .team {
    &-home {
      text-align: end;
      transform: translate(-80%, -700%);
    }

    &-guest {
      transform: translate(80%, 700%);
    }
  }

  .events{
    &-wrapper{
      &:after{
        width: 60vw;
        height: 60vw;
      }
    }
  }

  .swiper {
    width: 80%;

    &-slide {
      &-active {
        .events-item {
          transform: translateY(0) scale(1.5);
        }
      }

      &-prev {
        .events-item {
          transform: translateY(70%) scale(0.75);
        }
      }

      &-next {
        .events-item {
          transform: translateY(-70%) scale(0.75);
        }
      }
    }
  }
}

</style>
