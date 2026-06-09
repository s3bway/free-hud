<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const cwelun = ref(false)
const hujowsto = ref(100)
const underarmour = ref(100)
const mikrofonikbengbeng = ref(false)

function jebacfrajernie(e: MessageEvent) {
  const { type, action, value, active, data } = e.data

  if (type === 'zdrowkomordo' || (action === 'kasujecierandomie' && data?.health !== undefined)) {
    hujowsto.value = type === 'zdrowkomordo' ? value : data.health
  }

  if (type === 'batoniklajon' || (action === 'kasujecierandomie' && data?.armor !== undefined)) {
    underarmour.value = type === 'batoniklajon' ? value : data.armor
  }

  if (type === 'klikklikpapapa' || action === 'klikklikpapapa') {
    mikrofonikbengbeng.value = type === 'klikklikpapapa' ? active : data?.active ?? false
  }

  if (type === 'hellfieldatakuje') {
    cwelun.value = e.data.visible
  } else if (action === 'hellfieldatakuje') {
    cwelun.value = data
  }
}

onMounted(() => {
  window.addEventListener('message', jebacfrajernie)

  if (!(window as any).invokeNative) {
    cwelun.value = true
  }
})

onUnmounted(() => {
  window.removeEventListener('message', jebacfrajernie)
})
</script>

<template>
  <div
    v-if="cwelun"
    id="hud"
    class="fixed bottom-8 left-1/2 -translate-x-1/2 flex items-center gap-1.5"
  >
    <div
      id="hud-hujowsto"
      class="bengowanienakolanie"
      :class="{ 'border-red-500/40': hujowsto < 20 }"
    >
      <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M12 20.5L3.5 12C2.5 11 2 9.7 2 8.3 2 5.4 4.4 3 7.3 3c1.5 0 3 .7 4 1.9C12.3 3.7 13.7 3 15.3 3 18.2 3 20.6 5.4 20.6 8.3c0 1.4-.5 2.7-1.5 3.7L12 20.5Z"
          fill="white"
        />
        <polyline
          points="6,10 8,7 10,13 12,8 14,10 18,10"
          stroke="rgba(0,0,0,0.22)"
          stroke-width="1.1"
          stroke-linecap="round"
          stroke-linejoin="round"
          fill="none"
        />
      </svg>
    </div>

    <div
      id="hud-underarmour"
      class="bengowanienakolanie"
      :style="{ opacity: underarmour === 0 ? '0.3' : '1' }"
    >
      <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="3" y="7" width="18" height="14" rx="1.5" fill="white" />
        <rect x="4" y="3" width="5" height="6" rx="1" fill="white" />
        <rect x="15" y="3" width="5" height="6" rx="1" fill="white" />
        <path d="M9 3 Q12 5 15 3" fill="rgba(0,0,0,0.85)" />
        <rect x="4.5" y="9" width="2.5" height="4" rx="0.4" fill="rgba(0,0,0,0.18)" />
        <rect x="7.5" y="9" width="2.5" height="4" rx="0.4" fill="rgba(0,0,0,0.18)" />
        <rect x="14" y="9" width="2.5" height="4" rx="0.4" fill="rgba(0,0,0,0.18)" />
        <rect x="17" y="9" width="2.5" height="4" rx="0.4" fill="rgba(0,0,0,0.18)" />
        <line x1="12" y1="7" x2="12" y2="21" stroke="rgba(0,0,0,0.12)" stroke-width="1" />
        <rect x="5" y="15" width="6" height="4.5" rx="0.5" fill="rgba(0,0,0,0.13)" />
        <rect x="13" y="15" width="6" height="4.5" rx="0.5" fill="rgba(0,0,0,0.13)" />
        <rect x="10" y="9" width="4" height="4" rx="0.4" fill="rgba(0,0,0,0.1)" />
        <line x1="5" y1="17.5" x2="11" y2="17.5" stroke="rgba(0,0,0,0.1)" stroke-width="0.8" />
        <line x1="13" y1="17.5" x2="19" y2="17.5" stroke="rgba(0,0,0,0.1)" stroke-width="0.8" />
      </svg>
    </div>

    <div
      id="hud-mikrofonikbengbeng"
      class="bengowanienakolanie"
      :class="{ 'gadanieispiewanie': mikrofonikbengbeng }"
    >
      <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="8" y="2" width="8" height="13" rx="2" fill="white" />
        <line x1="8" y1="5.5" x2="16" y2="5.5" stroke="rgba(0,0,0,0.18)" stroke-width="0.9" />
        <line x1="8" y1="7.5" x2="16" y2="7.5" stroke="rgba(0,0,0,0.18)" stroke-width="0.9" />
        <line x1="8" y1="9.5" x2="16" y2="9.5" stroke="rgba(0,0,0,0.18)" stroke-width="0.9" />
        <line x1="8" y1="11.5" x2="16" y2="11.5" stroke="rgba(0,0,0,0.18)" stroke-width="0.9" />
        <rect x="16" y="5" width="2" height="4" rx="0.5" fill="white" />
        <path
          d="M5 11c0 3.87 3.13 7 7 7s7-3.13 7-7"
          stroke="white"
          stroke-width="1.8"
          stroke-linecap="round"
          fill="none"
        />
        <line x1="12" y1="18" x2="12" y2="21" stroke="white" stroke-width="1.8" stroke-linecap="round" />
        <line x1="9" y1="21" x2="15" y2="21" stroke="white" stroke-width="1.8" stroke-linecap="round" />
      </svg>
    </div>
  </div>
</template>

<style scoped>
.bengowanienakolanie {
  width: 52px;
  height: 52px;
  border-radius: 10px;
  background: rgba(15, 15, 15, 0.85);
  border: 1px solid rgba(255, 255, 255, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color 0.2s ease;
}

.bengowanienakolanie svg {
  width: 24px;
  height: 24px;
  filter: drop-shadow(0 0 4px rgba(255, 255, 255, 0.5));
}

.gadanieispiewanie svg {
  filter: drop-shadow(0 0 6px rgba(255, 255, 255, 0.9));
}
</style>
