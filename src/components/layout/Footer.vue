<template>
  <footer class="footer">
    <div class="container">
      <span class="logo">VOGUE<span class="gradient-text">&VEST</span></span>
      <p>&copy; {{ currentYear }} Vogue & Vest. Todos los derechos reservados.</p>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear();
</script>
