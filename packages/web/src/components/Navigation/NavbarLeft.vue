<template>
  <aside class="navbarLeft">
    <div
      class="h-screen w-navbarLeft pt-6 pb-5 flex flex-col bg-primary flex-shrink-0"
    >
      <div class="relative pb-2 flex items-center justify-center">
        <svg
          class="h-8 w-8 text-textLogo"
          viewBox="0 0 32 32"
          xmlns="http://www.w3.org/2000/svg"
          aria-hidden="true"
        >
          <defs>
            <linearGradient
              x1="108.695%"
              x2="12.439%"
              y1="-14.936%"
              y2="45.215%"
              id="uid11-1"
            >
              <stop stop-color="#DEEBFF" stop-opacity="0.4" offset="0%"></stop>
              <stop stop-color="#DEEBFF" offset="100%"></stop>
            </linearGradient>
            <linearGradient
              x1="0%"
              x2="91.029%"
              y1="118.55%"
              y2="63.971%"
              id="uid11-2"
            >
              <stop stop-color="#DEEBFF" stop-opacity="0.4" offset="0%"></stop>
              <stop stop-color="#DEEBFF" offset="100%"></stop>
            </linearGradient>
          </defs>
          <g>
            <path
              d="M15.967 29.362a6.675 6.675 0 0 0 0-9.442l-8.699-8.671-3.957 3.957a1.062 1.062 0 0 0 0 1.5l12.656 12.656zm12.656-14.156L15.967 2.55l-.039.039a6.675 6.675 0 0 0 .028 9.41l8.706 8.667 3.96-3.96a1.062 1.062 0 0 0 0-1.5z"
              fill="currentColor"
            ></path>
            <path
              d="M15.967 11.992a6.675 6.675 0 0 1-.028-9.41L6.91 11.606l4.72 4.721 4.336-4.335z"
              fill="url(#uid11-1"
            ></path>
            <path
              d="M20.295 15.591l-4.328 4.329a6.675 6.675 0 0 1 0 9.442l9.05-9.05-4.722-4.72z"
              fill="url(#uid11-2"
            ></path>
          </g>
        </svg>
      </div>

      <div
        v-for="(item, index) in items"
        :key="index"
        class="relative w-full flex items-center justify-center min-h-[42px]"
      >
        <div
          @click="item.handler"
          v-tippy="item.tooltip"
          class="itemIcon w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0 select-none transition-colors duration-100 cursor-pointer"
        >
          <j-icon class="text-white" :name="item.icon" :size="24"></j-icon>
        </div>
      </div>
      <div class="flex-auto"></div>
      <div
        class="relative w-full flex items-center justify-center min-h-[42px]"
      >
        <div
          v-tippy="currentUser.name"
          class="itemIcon w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0 select-none transition-colors duration-100 cursor-pointer"
        >
          <j-avatar
            :name="currentUser.name"
            :avatarUrl="currentUser.avatarUrl"
            :size="26"
          ></j-avatar>
        </div>
      </div>
      <div
        class="relative w-full flex items-center justify-center min-h-[42px]"
      >
        <div
          v-tippy="`About`"
          class="itemIcon w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0 select-none transition-colors duration-100 cursor-pointer"
        >
          <j-icon
            fill="transparant"
            class="text-white"
            name="help"
            :size="24"
          ></j-icon>
        </div>
      </div>
    </div>
  </aside>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue'
import eventBus from '@/utils/eventBus'
import { getters } from '../../store'
export default defineComponent({
  setup() {
    const currentUser = computed(getters.currentUser)
    const items = [
      {
        icon: 'search',
        tooltip: 'Search issue',
        handler: () => {
          eventBus.emit('toggle-issue-search', {
            isOpen: true
          })
        }
      },
      {
        icon: 'plus',
        tooltip: 'Create issue',
        handler: () => {
          eventBus.emit('toggle-issue-create', {
            isOpen: true
          })
        }
      }
    ]

    return {
      items,
      currentUser
    }
  }
})
</script>

<style lang="scss" scoped>
.itemIcon:hover {
  background: rgb(28, 99, 206);
}
</style>
