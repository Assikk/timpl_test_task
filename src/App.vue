<template>
  <div class="bg-[#F7F9FC]">

    <!-- Компонент списка иконок -->
    <Icons/>

    <!-- Компонент шапки -->
    <Header/>

    <!-- Начало блока слайдера -->
    <div class="mt-4">
       <swiper :slidesPerView="'auto'" :spaceBetween="30">
          <swiper-slide v-for="person in persons" :key="person.id">
            <div class="flex items-center justify-center gap-3">
              <img :src="person.avatar" :alt="person.name">
              <div class="font-semibold">
                <p class="text-[#0F0A2F] text-[22px] leading-[24px]">
                  {{person.name}}
                </p>
                <p class="text-[#9771FD]">
                  {{person.post}}
                </p>
              </div>
            </div>
          </swiper-slide>
        </swiper>
    </div>
    <!-- Конец блока слайдера -->
    <div class="px-5">
      <!-- Начало блока с суммой -->
      <section class="mt-5 mb-2 text-center pt-3 pb-[19px] bg-white rounded-[20px]">
        <h3 class="text-[15px] leading-[24px] font-medium">
          Enter amount of tips
        </h3>
        <h2 class="font-bold text-[34px] leading-[36px] pt-[5px]"
        :class="amount > 0 ? 'opacity-100 text-[#0F0A2F]' : 'opacity-10'">
          {{amount}}Є
        </h2>
      </section>
      <!-- Конец блока с суммой -->
      <section>
        <!-- Начало блока списка сумм -->
        <div class="flex gap-1">
          <div v-for="rate in rates" :key="rate.id" class="flex-1 text-center py-2 rounded-xl" :class="amount == rate.value ? 'bg-[#9771FD] text-[#fff]' : 'text-[#1F2A37] bg-white'"
          @click="amount = rate.value">
            <p class="font-semibold text-[13px] leading-[18px]">
              {{rate.name}}
            </p>
          </div>
        </div>
        <!-- Конец блока списка сумм -->
        <!-- Начало блока оценки опыта -->
        <div>
          <div class="flex items-center justify-center my-3">
            <div class="line"/>
            <h3 class="text-[15px] leading-[24px] font-medium mx-2">
              Rate your experience
            </h3>
            <div class="line"/>
          </div>
          <div class="py-4 flex gap-4 justify-center bg-white rounded-[20px]">
            <div v-for="star in stars" :key="star.id"
            @click="clickStar(star, stars)">
              <svg width="37" height="36" viewBox="0 0 37 36" :fill="star.isChecked ? '#9771FD' : '#CBD1D7'">
                <use xlink:href="#star"/>
              </svg>
            </div>
          </div>
        </div>
        <!-- Конец блока оценки опыта -->
        <!-- Начало блока оценки сервиса -->
        <div v-if="isShowServices">
          <div class="flex items-center justify-center my-3">
            <div class="line"/>
            <h3 class="text-[15px] leading-[24px] font-medium mx-2">
              Rate service
            </h3>
            <div class="line"/>
          </div>
          <div class="py-4 flex gap-4 justify-center bg-white rounded-[20px]">
            <div v-for="star in services" :key="star.id"
            @click="clickStar(star, services)">
              <svg width="37" height="36" viewBox="0 0 37 36" :fill="star.isChecked ? '#9771FD' : '#CBD1D7'">
                <use xlink:href="#star"/>
              </svg>
            </div>
          </div>
        </div>
        <!-- Конец блока оценки сервиса -->
        <!-- Начало блока выбора эмоджи -->
        <div v-if="isShowServices">
          <h3 class="text-[15px] leading-[24px] font-medium text-center mt-4 mb-3">
            What did you like?
          </h3>
          <div class="flex gap-3">
            <div v-for="item in emojis" :key="item.id" @click="item.isActive = !item.isActive">
              <img :src="item.isActive ? item.activeUrl : item.url" :alt="item.name">
              <p class="text-xs font-medium text-center"
              :class="item.isActive ? 'text-[#9771FD]' : 'text-[#808191]'">
                {{item.name}}
              </p>
            </div>
          </div>
        </div>
        <!-- Конец блока выбора эмоджи -->
        <!-- Старт блока обратной связи -->
        <div>
          <h3 class="text-[15px] leading-[24px] font-medium text-center mt-4 mb-3">
            Share your fedback
          </h3>
          <TextArea v-model="feedback" placeholder="Describe your own"/>
        </div>
        <!-- Конец блока обратной связи -->
      </section>
      <section class="mt-3 mb-[49px]">
        <div class="flex items-center justify-between gap-2 p-4">
          <div>
            <h4 class="font-medium text-lg w-3/4">
              I want Mark to receive the full amount
            </h4>
            <p class="text-xs text-[#808191] pr-5">
              You compensate service fee of 0.00€, which will be applied to your payment.
            </p>
          </div>
          <div class="w-[54px]">
            <Toggle/>
          </div>
        </div>
      </section>
    </div>
    <div class="bg-white px-5 rounded-[20px]">
      <!-- Начало блока оплаты -->
      <section>
          <div class="flex gap-4 items-center justify-between mb-6">
            <p class="text-[15px] leading-[24px] font-medium">
              To pay 0€
            </p>
            <p class="text-sm text-[#808191] font-medium">
              Service fees 0€
            </p>
          </div>
          <div class="flex flex-col gap-2">
            <Button @click="isShowModal = true">
              Pay with
              <template #next-icon>
                <svg width="48" height="24" iewBox="0 0 48 24" fill="white">
                  <use xlink:href="#pay"/>
                </svg>
              </template>
            </Button>
            <Button light>
              Pay with debit card
            </Button>
          </div>
      </section>
      <!-- Конец блока оплаты -->
      <!-- Футер компонент -->
      <Footer/>
    </div>
    <transition name="fade">
      <Modal v-if="isShowModal" @close="isShowModal = false"/>
    </transition>
  </div>
</template>
<script>
import Header from './components/header.vue'
import Toggle from './components/toggle.vue'
import Button from './components/buttons/default.vue'
import Footer from './components/footer.vue'
import Modal from './components/modals/swen.vue'
import Icons from './components/icons.vue'
import TextArea from './components/textarea.vue'
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/swiper-bundle.css';
export default {
  name: 'App',
  components: {
    Header,
    Toggle,
    Button,
    Footer,
    Icons,
    Swiper,
    SwiperSlide,
    Modal,
    TextArea
  },
  data() {
    return {
      amount: 0,
      rates: [
        {
          id: 1,
          name: '2',
          value: 20
        },
        {
          id: 2,
          name: '5',
          value: 50
        },
        {
          id: 3,
          name: '100',
          value: 100
        }
      ],
      stars: [
        {
          id: 1,
          isChecked: false
        },
        {
          id: 2,
          isChecked: false
        },
        {
          id: 3,
          isChecked: false
        },
        {
          id: 4,
          isChecked: false
        },
        {
          id: 5,
          isChecked: false
        }
      ],
      isShowServices: false,
      services: [
        {
          id: 1,
          isChecked: false
        },
        {
          id: 2,
          isChecked: false
        },
        {
          id: 3,
          isChecked: false
        },
        {
          id: 4,
          isChecked: false
        },
        {
          id: 5,
          isChecked: false
        }
      ],
      emojis: [
        {
          id: 1,
          url: '/img/emojis/service.svg',
          activeUrl: '/img/emojis/service-active.svg',
          isActive: false,
          name: 'Service'
        },
        {
          id: 2,
          url: '/img/emojis/cleanliness.svg',
          activeUrl: '/img/emojis/cleanliness.svg',
          isActive: false,
          name: 'Cleanliness'
        },
        {
          id: 3,
          url: '/img/emojis/atmosphere.svg',
          activeUrl: '/img/emojis/atmosphere-active.svg',
          isActive: false,
          name: 'Atmosphere'
        },
        {
          id: 4,
          url: '/img/emojis/food.svg',
          activeUrl: '/img/emojis/food.svg',
          isActive: false,
          name: 'Food quality'
        },
      ],
      persons: [
        {
          id: 1,
          avatar: '/img/persons/madison.png',
          name: 'Madison 1',
          post: 'Waiter 1'
        },
        {
          id: 2,
          avatar: '/img/persons/madison.png',
          name: 'Madison 2',
          post: 'Waiter 2'
        },
        {
          id: 3,
          avatar: '/img/persons/madison.png',
          name: 'Madison 3',
          post: 'Waiter 3'
        },
        {
          id: 4,
          avatar: '/img/persons/madison.png',
          name: 'Madison 4',
          post: 'Waiter 4'
        },
        {
          id: 5,
          avatar: '/img/persons/madison.png',
          name: 'Madison 5',
          post: 'Waiter 5'
        },
      ],
      isShowModal: false,
      feedback: ''
    }
  },
  methods: {
    clickStar(star, list) {
      this.isShowServices = true
      list.forEach((item) => {
        item.isChecked = false
        if(item.id <=  star.id) {
          item.isChecked = true
        }
      })
    }
  }
}
</script>
<style scoped>
.line {
  flex: 1;
  height: 1px;
  background: #9771FD;
}
</style>