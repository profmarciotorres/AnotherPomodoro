<template>
  <div>
    <transition name="transition-approximate-up" mode="out-in">
      <div :key="value" :class="['timer-approximate timer-display', { 'active': running }]">
        {{ value }}
      </div>
    </transition>
  </div>
</template>

<script>
import TimerMixin from '@/assets/mixins/timerMixin'

export default {
  mixins: [TimerMixin],
  computed: {
    value () {
      const lang = this.$store.state.settings.lang
      return this.$dayjs.formatRelative(this.timeOriginal - this.timeElapsed, {
        lang
      })
    }
  }
}
</script>

<style lang="scss" scoped>
div.timer-approximate {
  user-select: none;
  font-size: 8vw;
}

div.timer-approximate.transition-approximate-up-enter-active,
div.timer-approximate.transition-approximate-up-leave-active {
  transition: 300ms ease-out;
  transition-property: opacity, transform;
}

div.timer-approximate.transition-approximate-up-enter {
  opacity: 0 !important;
  transform: translateY(30px) !important;
}

div.timer-approximate.transition-approximate-up-leave-to {
  opacity: 0 !important;
  transform: translateY(-30px) !important;
}
</style>
