<template>
  <spinner-loading msg="true" v-if="oi"/>
  <div class="background-video-container" v-else>
    <video autoplay muted loop playsinline class="background-video">
      <source src="/video/climbeVideo.mp4" type="video/mp4" />
    </video>
    <div class="overlay">
      <div class="overlay-content">
        <image-component src="/img/climbe-logo.png" />
        <p>Portal do Sócio.</p>
        <div class="login-form">
          <input-component  placeholder="Digite seu email" v-model="user" required/>
          <input-component type="password" placeholder="Digite sua senha" v-model="pass" required/>
          <button-component />
        </div>
      </div>
      <hr />
      <div class="overlay-content">
        <image-component src="/img/climbe-logo.png" />
        <p>Portal do Sócio.</p>
        <div class="login-form">
          <input-component  placeholder="Digite seu email" v-model="user" required/>
          <input-component type="password" placeholder="Digite sua senha" v-model="pass" required/>
          <button-component />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ImageComponent from '@/components/ImageComponent.vue'
import InputComponent from '../components/InputComponent.vue'
import SpinnerLoading from '@/components/SpinnerLoading.vue';
import ButtonComponent from '@/components/ButtonComponent.vue';
export default {
  components: { ImageComponent, InputComponent, SpinnerLoading, ButtonComponent },
  data() {
    return {
      user: '',
      pass: ''
    }
  }
}
</script>

<style scoped>
.overlay {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid red !important;
  height: 100%;
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 16.5%;
}
.background-video-container {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.background-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.5);
  z-index: 0;
}

.background-video-container::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.3);
  pointer-events: none;
  z-index: 1;
}

.overlay-content {
  position: relative;
  z-index: 2;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 15px;
  color: #fff;
  text-align: center;
  padding: 0 1rem;
}

.overlay-content h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.overlay-content p {
  font-size: 1.25rem;
  max-width: 600px;
  line-height: 1.6;
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.6);
}

.overlay-content p {
  font-size: 24px;
}
</style>
