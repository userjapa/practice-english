<template>
  <div class="container">
    <div class="item">
      <div class="title">
        <h3>Listening</h3>
      </div>
      <div>
        <listening/>
      </div>
    </div>
    <div class="item">
      <div class="title">
        <h3>Pronunciation</h3>
      </div>
      <div>
        <pronunciation/>
      </div>
    </div>
  </div>
</template>
<script>
import listening from '@/components/Listening'
import pronunciation from '@/components/Pronunciation'

export default {
  name: "Listening",
  data: () => ({

  }),
  components: {
    listening,
    pronunciation
  }
}
</script>
<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  .item {
    align-self: center;
    flex-grow: 1;
    .title {
      text-align: center;
    }
  }
}
</style>
