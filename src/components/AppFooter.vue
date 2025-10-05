<template>
  <!-- Elegant Footer -->
  <footer class="bg-gradient-to-r from-gray-900 via-gray-800 to-gray-900 text-white py-12 relative overflow-hidden">
    <!-- Top Glow -->
    <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-teal-400 to-indigo-500 opacity-70"></div>

    <div class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-10 relative z-10">
      <!-- Main Footer Content -->
      <div class="flex flex-col md:flex-row justify-between items-center md:items-start gap-10">
        <!-- Brand Section -->
        <div class="text-center md:text-left">
          <h2 class="text-3xl font-bold text-teal-400 tracking-wide">Albert Garcia</h2>
          <p class="text-gray-400 mt-2 text-sm uppercase tracking-wider">Web Developer</p>
        </div>

        <!-- Social Links -->
        <div class="flex space-x-6">
          <a
            v-for="social in socialLinks"
            :key="social.icon"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-gray-400 hover:text-teal-400 transition transform hover:scale-110"
          >
            <i :class="`fab fa-${social.icon} text-2xl`"></i>
          </a>
        </div>
      </div>

      <!-- Divider -->
      <div class="border-t border-gray-700 mt-10 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
        <p class="text-gray-500 text-sm text-center md:text-left">
          © 2025 <span class="text-teal-400 font-medium">Albert Garcia</span>. All rights reserved.
        </p>

        <div class="flex space-x-6 text-sm">
          <a
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            class="text-gray-400 hover:text-teal-400 transition"
          >
            Privacy Policy
          </a>
          <a
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            class="text-gray-400 hover:text-teal-400 transition"
          >
            Terms of Service
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const socialLinks = [
  { icon: 'facebook-f', url: 'https://www.facebook.com/prince.burks.1' },
  { icon: 'linkedin-in', url: 'https://www.linkedin.com/in/asgdev/' },
  { icon: 'github', url: 'https://github.com/burks-bit' },
]
</script>

<style scoped>
footer {
  font-family: 'Inter', sans-serif;
  position: relative;
}
footer::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at top center, rgba(45, 212, 191, 0.05), transparent 70%);
  z-index: 0;
}
</style>
