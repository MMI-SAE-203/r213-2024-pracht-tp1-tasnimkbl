<script setup lang="ts">
import { ref } from 'vue'
const menuIsOpen = ref(false)
import { onErrorCaptured } from 'vue'
import { RouterLink, RouterView } from 'vue-router/auto'

onErrorCaptured((err, instance, info) => {
  console.error('erreur : ', err, '\ninfo : ', info, '\ncomposant : ', instance)
  return true
})
</script>

<template>
  <button @pointerdown="menuIsOpen = !menuIsOpen" aria-controls="mainNav" aria-expanded="true"
    class="rounded-full border-2 border-red-600 bg-red-300 px-2">
    menu
  </button>
  <!-- nav#mainNav>ul>li*3>a[href="#"]{item $} -->
  <Transition class="transition-transform duration-1000" enter-from-class="-translate-x-full"
    enter-to-class="translate-x-0" leave-active-class="-translate-x-full">
    <nav v-show="menuIsOpen" id="mainNav">
      <ul>
        <li>
          <RouterLink to="/" class="text-red-500 underline"> Accueil </RouterLink>
        </li>
        <li>
          <RouterLink to="/accordeon" class="text-red-500 underline"> Accordeon </RouterLink>
        </li>
      </ul>
    </nav>
  </Transition>
  <header>

  </header>
  <RouterView v-slot="{ Component }">
    <Suspense>
      <component :is="Component" />
    </Suspense>
  </RouterView>
</template>
