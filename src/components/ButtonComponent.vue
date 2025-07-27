<template>
  <button 
    class="button-loader" 
    :class="[customClass, { 'loading': isLoading, 'disabled': disabled }]" 
    :type="type"
    :disabled="disabled || isLoading"
    @click="handleClick"
  >
    <span class="button-text">
      {{ isLoading ? 'Carregando...' : text }}
    </span>
  </button>
</template>

<script>
export default {
  name: 'LoadingButton',
  props: {
    text: {
      type: String,
      default: 'Logar'
    },
    type: {
      type: String,
      default: 'button'
    },
    customClass: {
      type: [String, Array],
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    },
    loading: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isLoading: this.loading
    }
  },
  watch: {
    loading(newVal) {
      this.isLoading = newVal
    }
  },
  methods: {
    async handleClick(event) {
      if (!this.isLoading && !this.disabled) {
        this.isLoading = true
        this.$emit('click', event)
        
        // Se você quiser controlar o loading internamente, descomente as linhas abaixo:
        // try {
        //   await new Promise(resolve => setTimeout(resolve, 2000)) // Simula uma operação async
        // } finally {
        //   this.isLoading = false
        // }
      }
    }
  }
}
</script>

<style scoped>
.button-loader {
  border: none;
  outline: none;
  position: relative;
  padding: .75rem 2.5rem;
  background-color: var(--primary-color);
  color: var(--text-color);
  font-size: 1rem;
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-weight: 500;
  border-radius: 0.5rem;
  box-shadow: 0 8px 25px rgba(57, 198, 187, 0.3);
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s ease;
  min-width: 140px;
  text-align: center;
}

.button-loader:hover:not(.loading):not(.disabled) {
  background-color: var(--primary-color-alt);
  transform: translateY(-2px);
  box-shadow: 0 12px 35px rgba(57, 198, 187, 0.4);
}

.button-loader:active:not(.loading):not(.disabled) {
  transform: translateY(0);
}

.button-loader.loading {
  cursor: wait;
  pointer-events: none;
}

.button-loader.disabled {
  opacity: 0.6;
  cursor: not-allowed;
  pointer-events: none;
}

.button-loader.loading::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 150%;
  height: 100%;
  background: repeating-linear-gradient(
    60deg, 
    transparent, 
    transparent 0.75rem, 
    rgba(255, 255, 255, 0.1) 0.75rem, 
    rgba(255, 255, 255, 0.1) 1.5rem
  );
  animation: loading-animation 1s infinite linear;
  z-index: 1;
}

.button-text {
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.button-loader.loading .button-text::after {
  content: '';
  width: 16px;
  height: 16px;
  border: 2px solid transparent;
  border-top: 2px solid var(--text-color);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-left: 0.5rem;
}

@keyframes loading-animation {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(0);
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.button-loader:focus-visible {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}
</style>