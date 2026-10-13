<script setup>
import { ref } from 'vue'
import HomePage from './pages/HomePage.vue'
import ProfilePage from './pages/ProfilePage.vue'
import profileImage from '../assets/profile-B-8nHaKx.jpg'
import cert1 from '../assets/certificate1-BnDEoyBk.jpg'
import cert2 from '../assets/certificate2-BJrju29l.jpg'
import cert3 from '../assets/certificate3-B6DvxRGO.jpg'

const currentView = ref('home')
const contactTopOpen = ref(false)
const contactBottomOpen = ref(false)
const selectedCertificate = ref(null)

const certificates = [
  {
    title: 'Computer Hardware Basics',
    issuer: 'CTE / Training Center',
    year: '2023',
    image: cert1,
  },
  {
    title: 'Operating Systems Basics',
    issuer: 'ICT Academy',
    year: '2024',
    image: cert2,
  },
  {
    title: 'Introduction to Cybersecurity',
    issuer: 'IT Skills Program',
    year: '2025',
    image: cert3,
  },
]

const emailSubject = 'Portfolio Inquiry'
const emailBody =
  'Hello Ramram,\n\nI would like to get in touch with you regarding your portfolio.\n\nThank you.'

const profile = {
  name: 'Ramram C. Sanchez',
  course: 'BSIT 3rd Year',
  email: 'ramramsanchez1234@gmail.com',
  facebook: 'https://www.facebook.com/ramramsanchez1234/',
  gmailComposeUrl: `https://mail.google.com/mail/?${new URLSearchParams({
    view: 'cm',
    fs: '1',
    to: 'ramramsanchez1234@gmail.com',
    su: emailSubject,
    body: emailBody,
  })}`,
  mailtoUrl: `mailto:ramramsanchez1234@gmail.com?subject=${encodeURIComponent(emailSubject)}&body=${encodeURIComponent(emailBody)}`,
}

const viewProfile = () => {
  currentView.value = 'profile'
}

const backHome = () => {
  currentView.value = 'home'
}

const toggleTopContactMenu = () => {
  contactTopOpen.value = !contactTopOpen.value

  if (contactTopOpen.value) {
    contactBottomOpen.value = false
  }
}

const toggleBottomContactMenu = () => {
  contactBottomOpen.value = !contactBottomOpen.value

  if (contactBottomOpen.value) {
    contactTopOpen.value = false
  }
}

const openCertificate = (certificate) => {
  selectedCertificate.value = certificate
}

const closeCertificate = () => {
  selectedCertificate.value = null
}
</script>

<template>
  <div class="page-shell">
    <header class="topbar">
      <button class="brand" @click="viewProfile" aria-label="Open profile">
        <img :src="profileImage" alt="Profile" class="brand-photo" />
        <div class="brand-text">
          <span class="brand-name">{{ profile.name }}</span>
          <span class="brand-role">{{ profile.course }}</span>
        </div>
      </button>

      <div class="top-actions">
        <div class="contact-wrap">
          <button class="contact-toggle" @click="toggleTopContactMenu">Contact Me</button>
          <div v-if="contactTopOpen" class="contact-menu">
            <a :href="profile.gmailComposeUrl" target="_blank" rel="noopener noreferrer">Email with Gmail</a>
            <a :href="profile.mailtoUrl">Other email app</a>
            <a :href="profile.facebook" target="_blank" rel="noopener noreferrer">Facebook</a>
          </div>
        </div>

        <nav class="nav-links" aria-label="Main navigation">
          <button class="nav-link" @click="viewProfile">About Me</button>
        </nav>
      </div>
    </header>

    <main>
      <HomePage
        v-if="currentView === 'home'"
        :profile="profile"
        :profile-image="profileImage"
        :contact-open="contactBottomOpen"
        @open-profile="viewProfile"
        @toggle-contact="toggleBottomContactMenu"
      />

      <ProfilePage
        v-else
        :profile="profile"
        :profile-image="profileImage"
        :certificates="certificates"
        @back-home="backHome"
        @open-certificate="openCertificate"
      />
    </main>

    <div v-if="selectedCertificate" class="modal-overlay" @click="closeCertificate">
      <div class="modal-content" @click.stop>
        <button class="close-btn" @click="closeCertificate">×</button>
        <img :src="selectedCertificate.image" :alt="selectedCertificate.title" class="modal-image" />
        <div class="modal-text">
          <h4>{{ selectedCertificate.title }}</h4>
          <p>{{ selectedCertificate.issuer }} • {{ selectedCertificate.year }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
