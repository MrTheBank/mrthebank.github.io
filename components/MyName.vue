<template>
  <span class="type-it"></span>
</template>

<script>
import TypeIt from 'typeit';

export default {
  name: "MyName",
  mounted () {
    new TypeIt(this.$el, {
      speed: 50,
      afterComplete: function (instance) {
        instance.destroy();
      }
    })
      .type('Ponat')
      .move(-2)
      .type('lap')
      .move(null, { to: "END" })
      .type(' Ittiratchapong')
      .go()
    ;
  }
}
</script>
