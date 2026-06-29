<template>
  <header :class="{ 'scrolled': scrolled }">
    <h2 class="logo">Ijen <span>Bromo</span> Travel</h2>
    <nav :class="['navigation', { 'open': menuOpen }]">
      <router-link to="/" exact-active-class="active">Home</router-link>
      <router-link to="/about" exact-active-class="active">About</router-link>
      <a href="">Service</a>
      <a href="">Contact</a>
    </nav>
    <button class="menu-toggle" @click="menuOpen = !menuOpen" :class="{ 'open': menuOpen }">
      <span></span>
      <span></span>
      <span></span>
    </button>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import "../assets/css/landing.css";

const menuOpen = ref(false)
const scrolled = ref(false)
let handleScroll

onMounted(() => {
  handleScroll = () => {
    scrolled.value = window.scrollY > 50
  }
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>
