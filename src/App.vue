<template>
  <div id="app">
    <Navbar />
    <main>
      <Hero />
      <Features />
      <ContactForm />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import Navbar from './components/layout/Navbar.vue';
import Hero from './components/sections/Hero.vue';
import Features from './components/sections/Features.vue';
import ContactForm from './components/sections/ContactForm.vue';
import Footer from './components/layout/Footer.vue';
import './styles/main.css';
</script>
