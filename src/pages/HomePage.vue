<script setup>
import { computed } from 'vue'

const props = defineProps({
  profile: {
    type: Object,
    required: true,
  },
  profileImage: {
    type: String,
    required: true,
  },
  contactOpen: {
    type: Boolean,
    default: false,
  },
})

const emit = defineEmits(['toggle-contact'])

const fullName = computed(() => props.profile.name)
</script>

<template>
  <section class="hero">
    <div class="hero-content">
      <p class="eyebrow">Portfolio</p>
      <h1>Hi, I’m {{ fullName }}</h1>
      <h2>{{ profile.course }}</h2>
      <p class="intro">
        I am a student focused on information technology, programming, and digital solutions.
        I enjoy learning, building ideas, and creating meaningful work through technology.
      </p>
      <div class="hero-actions">
        <button class="primary-btn" @click="$emit('open-profile')">About Me</button>
        <button class="secondary-btn" @click="emit('toggle-contact')">Contact Me</button>
      </div>

      <div v-if="contactOpen" class="hero-contact-links">
        <a :href="profile.gmailComposeUrl" target="_blank" rel="noopener noreferrer">Email with Gmail</a>
        <a :href="profile.mailtoUrl">Other email app</a>
        <a :href="profile.facebook" target="_blank" rel="noopener noreferrer">Facebook</a>
      </div>
    </div>

    <div class="hero-visual">
      <div class="saturn-visual" aria-label="Saturn logo art">
        <div class="saturn-hero">
          <span class="saturn-core"></span>
          <span class="orbit orbit-one"></span>
          <span class="orbit orbit-two"></span>
          <span class="orbit orbit-three"></span>
        </div>
      </div>
    </div>
  </section>
</template>
