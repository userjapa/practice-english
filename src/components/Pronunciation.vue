<template>
  <div>
    <input type="text" name="text" v-model="text">
    <button type="button" name="speech" class="border-round" @click="speak()" ref="speech" :disabled="isTalking">Click to Speak</button>
    <input type="text" name="answer" v-model="answer" placeholder="You said..." disabled>
  </div>
</template>
<script>
export default {
  name: "pronunciation",
  data: () => ({
    text: "Are you all right?",
    voice: null,
    isTalking: false,
    answer: ''
  }),
  methods: {
    speak () {
      this.answer = ''
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
      this.$refs['speech'].style['background-color'] = 'red'
      this.$refs['speech'].style['color'] = 'white'
    }
    voice.onend = () => {
      console.log('Ended')
      this.isTalking = false
      this.$refs['speech'].style['background-color'] = 'white'
      this.$refs['speech'].style['color'] = 'black'
    }
    voice.onerror = err => {
      console.error('Error! ', err)
    }
    voice.onresult = ev => {
      let answer = ev.results[0][0].transcript
      let text = this.text

      // Set Answer
      this.answer = answer

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
.border-round {
  border-radius: 5 px;
}
</style>
