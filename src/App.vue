<template>
  <div class="word">
    <span v-for="(letter, idx) in word" :key="idx">
      <Word :letter="letter" :visible="getVisibleLetter(letter)" />
    </span>
  </div>

  <button type="button" :disabled="lettersDisabled.includes(letter)" v-for="(letter, index) in letters" :key="index" v-on:click="chooseLetter(letter)">{{ letter }}</button>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Word from './components/Word.vue';

@Options({
  components: { Word },
})
export default class App extends Vue {
  public letters: string[] = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']
  private words: string[] = ['ARTICHOKE','EGGPLANT','ASPARAGUS','CHICKPEAS','PEANUTS','PEAS','BROCCOFLOWER','BROCCOLI','CABBAGE','CAULIFLOWER','CELERY','ENDIVE','FIDDLEHEADS','FRISEE','FENNEL','KALE','SPINACH','ANISE','BASIL','CARAWAY','BASIL','CORIANDER','CHAMOMILE','OREGANO','PARSLEY','ROSEMARY']
  public matchLetters: string[] = []
  public lettersDisabled: string[] = []
  get generateWord(): string {
    return this.words[Math.floor(Math.random() * this.words.length)]
  }
  public word: string = this.generateWord
  public visible: boolean = false
  chooseLetter(letter: string): string {
    this.matchLetters.push(letter)
    this.lettersDisabled.push(letter)
    return letter
  }
  getVisibleLetter(letter: string): boolean {
    this.visible = this.matchLetters.includes(letter)
    return this.visible
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.word {
  margin-bottom: 24px;
}

button {
  margin: 6px;
  font-size: 24px;
}

span {
  margin-right: 10px;
  cursor: pointer;
}
</style>
