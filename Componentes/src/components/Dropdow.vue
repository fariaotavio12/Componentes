<template>
  <div class="dropdown" :style="styleObject" ref="dropdown" @click.stop>

    <div class="dropdown-header" @click="show = !show" @mouseover="addWidthToBeforeElement()" ref="elemento">
      <span class="dropdown-title">
        <slot name="title"></slot>
      </span>
      <i>
        <slot name="icon">
          <svg width="8" height="5" viewBox="0 0 8 5" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M0.497877 0.714623C0.636882 0.714623 0.775887 0.764324 0.87489 0.861154L3.999 3.9203L7.12311 0.861154C7.30512 0.682918 7.62113 0.664923 7.82913 0.820879C8.03714 0.976836 8.05814 1.24762 7.87614 1.42585L4.37601 4.85347C4.28101 4.94601 4.144 5 4 5C3.85599 5 3.71899 4.94687 3.62399 4.85347L0.123864 1.42585C-0.0581417 1.24762 -0.0371418 0.976836 0.170866 0.820879C0.265869 0.749756 0.382873 0.714623 0.499877 0.714623H0.497877Z" />
          </svg>
        </slot>

      </i>
      <!-- <span class="dropdown-icon">&#9660;</span> -->
    </div>
    <transition name="fade" :duration="550">
      <ul class="dropdown-list" v-if="show">
        <li :class="{ class_separator: separator.includes(index) }" v-for="(item, index) in dropdownList" :key="index">

          <a :href="
            //@ts-ignore
            item.href">{{
    //@ts-ignore
    item?.name }} </a>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

const props = defineProps({
  styleObject: {
    type: Object,
    default: () => ({})
  },
  dropdownTitle: {
    type: String,
    default: ''
  },
  dropdownList: {
    type: Array,
    default: () => []
  },
  separator: {
    type: Array,
    default: () => []
  },
  ativo: {
    type: Boolean,
    default: true
  }

})

const show = ref(false)
const showAjaxResult = ref(false);
const elementoRef = ref(null);

function handleClick(event: MouseEvent) {
  if (!(event.target as HTMLElement).classList.contains('dropdown')) {
    console.log('achou')
    show.value = false;
  }
}

onMounted(() => {
  document.addEventListener('click', handleClick);
  if (props.ativo) {
    const element = document.querySelector('.dropdown')

    const calculateHeight = () => {
      return `${100}%`
    }
    //@ts-ignore
    element.style.setProperty('--height', calculateHeight())
  }

});

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClick);
});

const addWidthToBeforeElement = async () => {
  const element = document.querySelector('.dropdown')
  //@ts-ignore
  element.style.setProperty('--height', '0')
}

</script>

<style scoped>
i {
  color: rgb(0, 0, 0);
  display: flex;
  padding: 2px;
  margin-left: 10px;
}

.dropdown {
  position: relative;
  width: auto;
  height: 30px;
  font-size: 16px;
  color: #333;
  background-color: aliceblue;
}



.dropdown-header {
  display: flex;
  align-items: center;
  justify-content: start;
  padding: 5px 7px;
  border-radius: 4px;
  cursor: pointer;
}

.dropdown-header::before {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  height: 2px;
  width: var(--height, 0);
  background-color: #3b92e8;
  transition: width 0.5s ease;
}

.dropdown-header:hover::before {
  width: 100%;
}

.dropdown-title {
  width: auto;
}

.dropdown-icon {
  margin-left: 5px;
  font-size: 12px;
}

.dropdown-list {
  position: absolute;
  top: 125%;
  left: 0px;
  width: 100%;
  min-width: 150px;
  max-height: 150px;
  overflow-x: hidden;
  overflow-y: auto;
  margin: 0;
  padding: 0;
  border: 1px solid #ccc;
  border-radius: 4px 4px 4px 4px;
  background-color: aliceblue;
  list-style-type: none;
  display: flex;
  word-wrap: break-word;
  flex-direction: column;
}

.dropdown-list li {
  margin-top: 4px;
  margin-bottom: 4px;
  padding: 3px 16px;
  cursor: pointer;
}

.dropdown-list li a {
  text-decoration: none;
  color: #333;
}


.dropdown-list li:hover {
  background-color: #cccbcb;
  border-radius: 4px;
}

.class_separator::before {
  content: "";
  position: absolute;
  left: 0;
  top: -4px;
  height: 1px;
  width: 100%;
  background-color: #a19d9d;
  transition: width 0.5s ease;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity .8s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>