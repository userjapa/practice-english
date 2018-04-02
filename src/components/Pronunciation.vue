<template>
  <div>
    <input type="text" name="text" v-model="text">
    <button type="button" name="speech" @click="speak()" :disabled="isTalking">Click to Speak</button>
  </div>
</template>
<script>
export default {
  name: "",
  data: () => ({
    text: "Are you alright?",
    voice: null,
    isTalking: false
  }),
  methods: {
    speak () {
      this.isTalking = true
      this.voice.start()
    }
  },
  beforeMount () {
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition

    let voice = new SpeechRecognition()
    voice.lang = 'en-US'
    voice.interimResults = false
    voice.maxAlternatives = 5
    voice.onaudiostart = () => {
      console.log('Getting voice...')
    }
    voice.onend = () => {
      console.log('Ended')
      this.isTalking = false
    }
    voice.onerror = err => {
      console.error('Error! ', err)
    }
    voice.onresult = ev => {
      let answer = ev.results[0][0].transcript
      let text = this.text

      answer = answer.replace(/[\.?!,]+/g, '').toLowerCase().trim()
      text = text.replace(/[\.?!,]+/g, '').toLowerCase().trim()
      console.log(answer)
      if (answer === text) alert('Correct!')
      else alert('You Failed!')
    }
    this.voice = voice
  }
}
</script>
<style lang="scss" scoped>
</style>
