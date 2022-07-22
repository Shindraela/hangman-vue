<template>
  <span>{{ visible ? letter : '_' }}</span>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component"

@Options({
  props: {
    letter: String,
    visible: Boolean
  }
})

export default class Word extends Vue {
  letter!: string
  visible!: boolean
}
</script>

<style scoped>
  span {
    font-size: 24px;
  }
</style>
