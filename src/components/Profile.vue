<template>
  <!-- HEADER -->
  <header class="fixed top-0 w-full z-50 bg-white dark:bg-gray-900 shadow">
    <nav class="container mx-auto flex items-center justify-between p-4">
      <h1 class="text-xl font-bold">Family Calendar App</h1>

      <!-- Hamburger Menu -->
      <button class="md:hidden" @click="toggleMobileMenu">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none"
          viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round"
            stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>

      <!-- Desktop Nav -->
      <ul class="hidden md:flex space-x-6">
        <li v-for="link in navItems" :key="link">
          <a :href="'#' + link.toLowerCase()" class="text-gray-700 hover:text-blue-500"
            @click="scrollToSection(link)">
            {{ link }}
          </a>
        </li>
      </ul>
    </nav>

    <!-- Mobile Nav -->
    <ul v-if="isMobileMenuVisible"
      class="md:hidden bg-white dark:bg-gray-900 px-4 pb-4 space-y-2">
      <li v-for="link in navItems" :key="link">
        <a :href="'#' + link.toLowerCase()" class="block text-gray-700 hover:text-blue-500"
          @click="handleMobileNavClick(link)">
          {{ link }}
        </a>
      </li>
    </ul>
  </header>

  <!-- HERO -->
  <section
    class="relative flex items-center justify-center text-center text-white overflow-hidden py-28 md:py-40 hero-gradient">
    <div class="absolute inset-0 bg-gradient-to-r from-teal-600 via-indigo-700 to-orange-800 animate-gradient-x"></div>
    <div class="absolute top-20 left-10 w-40 h-40 bg-teal-400 rounded-full blur-3xl opacity-30"></div>
    <div class="absolute bottom-16 right-12 w-48 h-48 bg-indigo-500 rounded-full blur-3xl opacity-30"></div>
    <div class="relative z-10 backdrop-blur-md bg-white/10 border border-white/20 rounded-2xl shadow-2xl px-8 py-12 max-w-3xl mx-4">
      <h1 class="text-5xl md:text-6xl font-extrabold tracking-tight mb-4 bg-clip-text text-transparent bg-gradient-to-r from-teal-300 to-indigo-400 animate-fade-in-down">
        Family Calendar App
      </h1>
      <p class="text-lg md:text-xl text-white/80 font-light animate-fade-in mb-8">
        Stay connected with your loved ones — track birthdays and cherish family moments.
      </p>
      <a href="#family"
        class="inline-block bg-teal-500 hover:bg-teal-600 text-white font-semibold py-3 px-8 rounded-full shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300">
        View Family Members
      </a>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about" class="py-16 bg-white">
    <div class="max-w-6xl mx-auto px-4 text-center">
      <h2 class="text-3xl font-bold mb-6">About This App</h2>
      <p class="text-lg">
        This app helps you monitor and remember the birthdates of your family members.
      </p>
    </div>
  </section>

  <!-- FAMILY MEMBERS -->
  <section id="family" class="py-16 bg-gray-50">
    <div class="max-w-6xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-center mb-8">Family Members</h2>

      <div class="flex justify-center mb-10">
        <div class="w-full md:w-1/3">
          <label for="familyFilter" class="block text-gray-700 font-medium mb-2">Family Name</label>
          <select id="familyFilter" v-model="selectedFamily"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-2 focus:ring-indigo-500 focus:outline-none">
            <option value="">All Families</option>
            <option v-for="family in familyNames" :key="family" :value="family">{{ family }}</option>
          </select>
        </div>
      </div>

      <ul class="space-y-4">
        <li v-for="member in filteredMembers" :key="member.name"
          class="flex items-center justify-between bg-white p-5 rounded-xl shadow hover:shadow-lg transition-all duration-300">
          <div class="flex items-center gap-4">
            <div class="bg-teal-100 p-1 rounded-full flex items-center justify-center">
              <img v-if="member.gender === 'Male'" src="/male.png" alt="Male" class="h-8 w-8 object-cover" />
              <img v-else-if="member.gender === 'Female'" src="/female.png" alt="Female" class="h-8 w-8 object-cover" />
            </div>
            <div>
              <p class="text-lg font-semibold text-gray-800">{{ member.name }}</p>
              <p class="text-sm text-gray-500">{{ member.family }}</p>
            </div>
          </div>

          <button @click="openDetails(member)"
            class="px-4 py-2 bg-indigo-500 text-white font-medium rounded-md shadow hover:shadow-lg hover:bg-indigo-800 active:scale-95 transition-all duration-200 text-sm md:text-base md:px-5">
            <span class="fa fa-eye"></span> &nbsp;
            View
          </button>
        </li>
      </ul>
    </div>
  </section>

  <!-- UPCOMING BIRTHDAYS -->
  <section id="birthdays" class="py-16 bg-gradient-to-r from-indigo-50 to-indigo-50">
    
    <div v-if="upcomingBirthdays.length > 0" class="max-w-6xl mx-auto px-4 text-center">
      <h2 class="text-3xl font-bold text-gray-800 mb-8">🎂 Upcoming Birthdays</h2>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="member in upcomingBirthdays" :key="member.name"
          class="bg-white rounded-xl shadow-lg p-6 hover:shadow-2xl transition duration-300 border border-gray-100">
          <div class="flex flex-col items-center">
            <img v-if="member.gender === 'Male'" src="/male.png" class="h-16 w-16 rounded-full mb-4" />
            <img v-else-if="member.gender === 'Female'" src="/female.png" class="h-16 w-16 rounded-full mb-4" />
            <h3 class="text-xl font-semibold text-gray-800">{{ member.name }}</h3>
            <p class="text-gray-500 text-sm mb-2">{{ member.family }}</p>
            <p class="text-indigo-600 font-medium">{{ formatBirthdate(member.birthdate) }}</p>
            <p class="text-sm text-gray-600 mt-1">🎉 In {{ daysUntilBirthday(member.birthdate) }} days</p>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="max-w-6xl mx-auto px-4 text-center">
      <h2 class="text-3xl font-bold text-gray-800 mb-8">🎂 Upcoming Birthdays</h2>
      <p class="text-gray-600 mt-1">
            upcoming birthdays in the next 30 days.
          </p>
    </div>
  </section>

  <!-- DIALOG -->
  <transition name="fade-zoom">
    <div v-if="isDialogVisible" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
      <div
      class="bg-white p-6 rounded-2xl shadow-2xl w-full max-w-sm relative text-center"
    >
      <!-- Close Button -->
      <button
        class="absolute top-2 right-3 text-gray-400 hover:text-gray-700 text-2xl font-bold"
        @click="closeDetails"
      >
        &times;
      </button>

      <!-- Avatar -->
      <div class="flex justify-center mb-4">
        <div
          class="bg-indigo-100 p-3 rounded-full flex items-center justify-center w-28 h-28"
        >
          <img
            v-if="selectedMember.gender === 'Male'"
            src="/male.png"
            alt="Male"
            class="h-24 w-24 object-cover rounded-full"
          />
          <img
            v-else-if="selectedMember.gender === 'Female'"
            src="/female.png"
            alt="Female"
            class="h-24 w-24 object-cover rounded-full"
          />
          <svg
            v-else
            xmlns="http://www.w3.org/2000/svg"
            class="h-12 w-12 text-indigo-600"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M5.121 17.804A9 9 0 1118.364 4.56 9 9 0 015.121 17.804z"
            />
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
            />
          </svg>
        </div>
      </div>

      <!-- Profile Info -->
      <h2 class="text-2xl font-bold text-gray-800 mb-2">
        {{ selectedMember.name }}
      </h2>
      <p class="text-sm text-gray-500 mb-4">
        <span class="inline-flex items-center gap-1">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M5.121 17.804A9 9 0 1118.364 4.56 9 9 0 015.121 17.804z" />
          </svg>
          {{ selectedMember.gender }}
        </span>
        •
        <span class="inline-flex items-center gap-1">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          {{ computeAge(selectedMember.birthdate) }}
        </span>
      </p>

      <!-- Details with Icons -->
      <div class="space-y-3 text-left text-gray-700">
        <p class="flex items-center gap-2">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M8 7V3m8 4V3m-9 8h10m-12 4h14m-14 4h14m-14 4h14" />
          </svg>
          <span><strong>Birthdate:</strong> {{ selectedMember.birthdate }}</span>
        </p>

        <p class="flex items-center gap-2">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M17.657 16.657L13.414 12.414a4 4 0 10-5.657 5.657L16.657 17.657z" />
          </svg>
          <span><strong>Birthplace:</strong> {{ selectedMember.birthplace }}</span>
        </p>

        <p class="flex items-center gap-2">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-indigo-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M3 9l9 6 9-6-9-6-9 6z" />
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M21 9v6a9 9 0 11-18 0V9" />
          </svg>
          <span><strong>Family:</strong> {{ selectedMember.family }}</span>
        </p>
      </div>
    </div>
    </div>
  </transition>
</template>

<script setup>
import { ref, computed } from "vue";

const isMobileMenuVisible = ref(false);
const navItems = ["Home", "About", "Family", "Birthdays"];

const toggleMobileMenu = () => (isMobileMenuVisible.value = !isMobileMenuVisible.value);
const scrollToSection = (id) => {
  const section = document.getElementById(id.toLowerCase());
  if (section) section.scrollIntoView({ behavior: "smooth" });
};
const handleMobileNavClick = (id) => {
  scrollToSection(id);
  isMobileMenuVisible.value = false;
};

// FAMILY DATA
const familyMembers = ref([
  { name: "Albert Garcia", birthdate: "April 8, 1997", birthplace: "Muntinlupa City", family: "Garcia", gender: "Male" },
  { name: "April Rose Garcia", birthdate: "September 12, 1999", birthplace: "Legazpi City", family: "Garcia", gender: "Female" },
  { name: "Daine Macalintal", birthdate: "July 30, 1997", birthplace: "San Pablo City, Laguna", family: "Macalintal", gender: "Female" }
]);

const familyNames = ["Serrano", "Garcia", "Macalintal"];
const selectedFamily = ref("");

const filteredMembers = computed(() => {
  if (!selectedFamily.value) return familyMembers.value;
  return familyMembers.value.filter((m) => m.family === selectedFamily.value);
});

// UPCOMING BIRTHDAYS
const daysUntilBirthday = (birthdate) => {
  const today = new Date();
  const birthday = new Date(birthdate);
  birthday.setFullYear(today.getFullYear());
  if (birthday < today) birthday.setFullYear(today.getFullYear() + 1);
  return Math.ceil((birthday - today) / (1000 * 60 * 60 * 24));
};

const upcomingBirthdays = computed(() => {
  return familyMembers.value
    .map((m) => ({ ...m, daysLeft: daysUntilBirthday(m.birthdate) }))
    .filter((m) => m.daysLeft <= 30)
    .sort((a, b) => a.daysLeft - b.daysLeft);
});

const formatBirthdate = (dateStr) => {
  const date = new Date(dateStr);
  return date.toLocaleDateString("en-US", { month: "long", day: "numeric" });
};

// DIALOG
const isDialogVisible = ref(false);
const selectedMember = ref({});
const openDetails = (member) => {
  selectedMember.value = member;
  isDialogVisible.value = true;
};
const closeDetails = () => (isDialogVisible.value = false);

// AGE COMPUTATION
const computeAge = (birthdate) => {
  const birth = new Date(birthdate)
  const today = new Date()

  let years = today.getFullYear() - birth.getFullYear()
  let months = today.getMonth() - birth.getMonth()
  let days = today.getDate() - birth.getDate()

  if (days < 0) {
    months--
    days += new Date(today.getFullYear(), today.getMonth(), 0).getDate()
  }
  if (months < 0) {
    years--
    months += 12
  }

  return `${years} years, ${months} months, ${days} days`
}
</script>

<style>
html {
  scroll-behavior: smooth;
}
.hero-gradient {
  background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
}
.fade-zoom-enter-active,
.fade-zoom-leave-active {
  transition: all 0.5s ease;
}
.fade-zoom-enter-from,
.fade-zoom-leave-to {
  opacity: 0;
  transform: scale(0.95);
}
.fade-zoom-enter-to,
.fade-zoom-leave-from {
  opacity: 1;
  transform: scale(1);
}
@keyframes gradient-x {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
.animate-gradient-x {
  background-size: 200% 200%;
  animation: gradient-x 10s ease infinite;
}
@keyframes fade-in-down {
  0% { opacity: 0; transform: translateY(-20px); }
  100% { opacity: 1; transform: translateY(0); }
}
.animate-fade-in-down { animation: fade-in-down 1s ease forwards; }
</style>
