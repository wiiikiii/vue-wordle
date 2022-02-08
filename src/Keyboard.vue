<script setup lang="ts">
import { LetterState } from './types'

defineProps<{
  letterStates: Record<string, LetterState>
}>()

defineEmits<{
  (e: 'key', key: string): void
}>()

const rows = [
  'qwertzuiop'.split(''),
  'asdfghjkl'.split(''),
  ['Enter', ...'yxcvbnm'.split(''), 'Backspace']
]
</script>

<template>
  <div id="keyboard">
    <div class="row" v-for="(row, i) in rows" :key="i">
      <div class="spacer" v-if="i === 1"></div>
      <button
        v-for="( key, i ) in row" :key="i"
        :class="[key.length > 1 && 'big', letterStates[key]]"
        @click="$emit('key', key)"
      >
        <svg v-if="key == 'Backspace'"
          xmlns="http://www.w3.org/2000/svg"
          height="24"
          viewBox="0 0 24 24"
          width="24"
        >
          <path
            fill="currentColor"
            d="M22 3H7c-.69 0-1.23.35-1.59.88L0 12l5.41 8.11c.36.53.9.89 1.59.89h15c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm0 16H7.07L2.4 12l4.66-7H22v14zm-11.59-2L14 13.41 17.59 17 19 15.59 15.41 12 19 8.41 17.59 7 14 10.59 10.41 7 9 8.41 12.59 12 9 15.59z"
          ></path>
        </svg>
        <svg v-else-if="key == 'Enter'"
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24" >
          <g transform="matrix(1.48371,0,0,1.48371,-5.50891,-7.26436)">
              <path d="M15.429,12.36L10.334,12.36L11.391,11.303L9.862,9.775L6.251,13.386L6.267,13.402L6.266,13.403L7.347,14.484L7.347,14.521L7.385,14.521L9.949,17.085L11.477,15.557L10.442,14.521L17.553,14.521L17.553,14.464L17.591,14.464L17.591,9.508L15.429,9.508L15.429,12.36ZM6.556,14.56L6.562,14.943L6.551,14.943L6.556,14.56Z"/>
          </g>
        </svg>
        <span v-else>{{ key }}</span>
      </button>
      <div class="spacer" v-if="i === 1"></div>
    </div>
  </div>
</template>

<style scoped>
#keyboard {
  position: absolute;
  bottom: 0;
  width: min(500px, 98%);
  margin: 30px 8px 0;
  user-select: none;
}
.row {
  display: flex;
  width: 100%;
  margin: 0 auto 8px;
  touch-action: manipulation;
}
.spacer {
  flex: 0.5;
}
button {
  font-family: inherit;
  font-weight: bold;
  font-size: 16px;
  border: 0;
  padding: 0;
  margin: 0 6px 0 0;
  height: 58px;
  border-radius: 4px;
  cursor: pointer;
  user-select: none;
  background-color: #d3d6da;
  color: #1a1a1b;
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0.3);
  transition: all 0.2s 1.5s;
}
button:last-of-type {
  margin: 0;
}
button.big {
  flex: 1.5;
}
</style>
