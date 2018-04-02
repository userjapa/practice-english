<template>
  <div>
    <button type="button" name="speech" @click="speak()">Listen</button>
    <input type="text" name="text" v-model="answer">
    <button type="button" name="verify" @click="verify(answer, text)"
    >Check</button>
  </div>
</template>
<script>
export default {
  name: "listening",
  data: () => ({
    text: 'Are you ok?',
    language: {},
    voice: speechSynthesis,
    answer: ''
  }),
  methods: {
    speak () {
      const speech = new SpeechSynthesisUtterance(this.text)
      speech.voice = this.language
      this.voice.speak(speech)
    },
    verify (answer, text) {
      answer = answer.replace(/[\.?!,]/g, '').toLowerCase().trim()
      text = text.replace(/[\.?!,]+/g, '').toLowerCase().trim()
      if (answer === text) alert('Correct!')
      else alert('You Failed!')
      this.answer = ''
    }
  },
  beforeMount () {
    let languages = []
    let english = {}
    setTimeout(() => {
      languages = this.voice.getVoices()
      this.language = languages.filter(x => x.lang === 'en-US')[2]
    }, 10)
  }
}
</script>
<style lang="scss" scoped>
</style>
