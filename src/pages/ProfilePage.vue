<script setup>
const props = defineProps({
  profile: {
    type: Object,
    required: true,
  },
  profileImage: {
    type: String,
    required: true,
  },
  certificates: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['back-home', 'open-certificate'])

function openCertificate(certificate) {
  emit('open-certificate', certificate)
}
</script>

<template>
  <section class="profile-page">
    <button class="back-btn" @click="$emit('back-home')">← Back Home</button>

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
          <div>
            <strong>Email:</strong>
            <a :href="profile.gmailComposeUrl" target="_blank" rel="noopener noreferrer">Compose in Gmail</a>
            <span> · </span>
            <a :href="profile.mailtoUrl">Use another email app</a>
            <span class="email-address">({{ profile.email }})</span>
          </div>
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
</template>
