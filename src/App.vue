<script setup>
import { ref } from 'vue'
import profileImage from './assets/profile-B-8nHaKx.jpg'
import cert1 from './assets/certificate1-BnDEoyBk.jpg'
import cert2 from './assets/certificate2-BJrju29l.jpg'
import cert3 from './assets/certificate3-B6DvxRGO.jpg'

const currentView = ref('home')
const contactOpen = ref(false)
const selectedCertificate = ref(null)

const certificates = [
  {
    title: 'BSIT Fundamentals',
    issuer: 'CTE / Training Center',
    year: '2023',
    image: cert1,
  },
  {
    title: 'Web Development',
    issuer: 'ICT Academy',
    year: '2024',
    image: cert2,
  },
  {
    title: 'Computer Programming',
    issuer: 'IT Skills Program',
    year: '2025',
    image: cert3,
  },
]

const profile = {
  name: 'Sanchez',
  course: 'BSIT 3rd Year',
  email: 'ramramsanchez1234@gmail.com',
  facebook: 'https://www.facebook.com/ramramsanchez1234',
}

const viewProfile = () => {
  currentView.value = 'profile'
}

const backHome = () => {
  currentView.value = 'home'
}

const toggleContactMenu = () => {
  contactOpen.value = !contactOpen.value
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
        <div class="brand-mark">
          <span class="saturn-core"></span>
          <span class="orbit orbit-one"></span>
          <span class="orbit orbit-two"></span>
        </div>
        <div class="brand-text">
          <span class="brand-name">{{ profile.name }}</span>
          <span class="brand-role">{{ profile.course }}</span>
        </div>
      </button>

      <div class="top-actions">
        <div class="contact-wrap">
          <button class="contact-toggle" @click="toggleContactMenu">Contact Me</button>
          <div v-if="contactOpen" class="contact-menu">
            <a :href="`mailto:${profile.email}`">Email</a>
            <a :href="profile.facebook" target="_blank" rel="noopener noreferrer">Facebook</a>
          </div>
        </div>
      </div>
    </header>

    <main>
      <section v-if="currentView === 'home'" class="hero">
        <div class="hero-content">
          <p class="eyebrow">Portfolio</p>
          <h1>Hi, I’m {{ profile.name }}</h1>
          <h2>{{ profile.course }}</h2>
          <p class="intro">
            I am a student focused on information technology, programming, and digital solutions.
            I enjoy learning, building ideas, and creating meaningful work through technology.
          </p>
          <div class="hero-actions">
            <button class="primary-btn" @click="viewProfile">View Profile</button>
            <button class="secondary-btn" @click="toggleContactMenu">Contact Me</button>
          </div>
        </div>

        <div class="hero-visual">
          <div class="photo-card">
            <img :src="profileImage" :alt="profile.name" class="profile-photo" />
          </div>
        </div>
      </section>

      <section v-else class="profile-page">
        <button class="back-btn" @click="backHome">← Back Home</button>

        <div class="profile-header">
          <div class="profile-photo-box">
            <img :src="profileImage" :alt="profile.name" class="profile-image-large" />
          </div>

          <div class="profile-info">
            <p class="section-tag">About Me</p>
            <h3>{{ profile.name }}</h3>
            <p class="role-line">{{ profile.course }}</p>
            <p>
              A BSIT student passionate about learning new technologies, creating digital experiences,
              and developing both technical and creative skills for future opportunities.
            </p>
            <div class="info-list">
              <div><strong>Email:</strong> <a :href="`mailto:${profile.email}`">{{ profile.email }}</a></div>
              <div>
                <strong>Facebook:</strong>
                <a :href="profile.facebook" target="_blank" rel="noopener noreferrer">View profile</a>
              </div>
            </div>
          </div>
        </div>

        <div class="certificate-section">
          <div class="section-title-row">
            <p class="section-tag">Certificates</p>
            <h4>My Achievements</h4>
          </div>

          <div class="certificate-grid">
            <article v-for="(certificate, index) in certificates" :key="index" class="certificate-card">
              <button class="certificate-button" @click="openCertificate(certificate)">
                <img :src="certificate.image" :alt="certificate.title" />
              </button>
              <div class="certificate-caption">
                <h5>{{ certificate.title }}</h5>
                <span>{{ certificate.issuer }} • {{ certificate.year }}</span>
              </div>
            </article>
          </div>
        </div>
      </section>
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
