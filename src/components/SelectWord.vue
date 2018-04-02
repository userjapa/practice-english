<template>
  <div>
    <div>
      <p>I used to <span class="correct" ref="word">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span> breakfast everyday.</p>
    </div>
    <div class="options">
      <span @click="choose($event)">HAVE</span>
      <span @click="choose($event)">HAS</span>
      <span @click="choose($event)">HAD</span>
    </div>
  </div>
</template>
<script>
export default {
  name: "selectWord",
  methods: {
    choose (ev) {
      const word = ev.target.textContent
      if (word === 'HAVE') {
        this.$refs['word'].textContent = word
        ev.target.textContent = ''
        alert('Correct!')
      } else {
        alert('You HAVE failed!')
      }
    }
  }
}
</script>
<style lang="scss" scoped>
  .correct {
    min-width: 20px;
    border-bottom: 1px solid black;
    width: 50px;
    border-bottom: 2px solid black;
    font-weight: bold;
  }

  .options {
    display: flex;
    justify-content: center;
  }

  .options span {
    align-self: center;
    flex-grow: 1;
    font-weight: bold;
    border: 1px solid white;
    border-radius: 10px;
  }

  .options span:hover {
    border-color: black;
    cursor: pointer;
  }
</style>
