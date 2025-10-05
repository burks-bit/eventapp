<template>
  <div id="projects" class="bg-white py-24 sm:py-32 lg:py-40">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="sm:flex sm:items-center sm:justify-between">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">My Projects</h2>
        <a href="#" class="mt-6 inline-flex items-center gap-x-1 text-sm font-semibold leading-6 text-indigo-600 sm:mt-0">
          View all projects
          <svg class="h-5 w-5 text-indigo-500" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
            <path fill-rule="evenodd" d="M12.03 4.97a.75.75 0 011.06 0l5 5a.75.75 0 010 1.06l-5 5a.75.75 0 01-1.06-1.06L15.44 11H3a.75.75 0 010-1.5h12.44l-3.41-3.47a.75.75 0 010-1.06z" clip-rule="evenodd" />
          </svg>
        </a>
      </div>

      <div class="mt-10 space-y-20 lg:mt-16 lg:space-y-20">
        <article class="relative isolate flex flex-col gap-8 lg:flex-row">
          <div class="relative aspect-[16/9] w-full flex-none sm:aspect-[2/1] lg:aspect-square lg:w-64 lg:shrink-0">
            <img src="https://tailwindui.com/img/component-images/project-app-screenshot.png" alt="" class="absolute inset-0 h-full w-full rounded-2xl bg-gray-50 object-cover" />
            <div class="absolute inset-0 rounded-2xl ring-1 ring-inset ring-gray-900/10"></div>
          </div>
          <div>
            <div class="flex items-center gap-x-4 text-xs">
              <time datetime="2023-03-16" class="text-gray-500">Mar 16, 2023</time>
              <a href="#" class="relative z-10 rounded-full bg-gray-50 px-3 py-1.5 font-medium text-gray-600 hover:bg-gray-100">Marketing</a>
            </div>
            <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900">
              <a href="#">
                <span class="absolute inset-0"></span>
                Project name goes here
              </a>
            </h3>
            <p class="mt-5 text-sm leading-6 text-gray-600">
              This is a short summary or description of the project. It should be catchy and informative.
            </p>
            <div class="mt-6 flex border-t border-gray-900/5 pt-6">
              <div class="relative flex items-center gap-x-4">
                <img src="https://tailwindui.com/img/component-images/avatar.jpg" alt="" class="h-10 w-10 rounded-full bg-gray-50" />
                <div class="text-sm leading-6">
                  <p class="font-semibold text-gray-900">
                    <a href="#">
                      <span class="absolute inset-0"></span>
                      Author Name
                    </a>
                  </p>
                  <p class="text-gray-600">Role or Position</p>
                </div>
              </div>
            </div>
          </div>
        </article>
        <!-- Repeat article blocks as needed -->
      </div>
    </div>
  </div>
</template>

<script setup>
// No logic needed unless dynamic content is desired
</script>

<style scoped>
/* Keep it empty or add custom styles as needed */
</style>
