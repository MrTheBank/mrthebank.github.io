<template>
  <span class="type-it"></span>
</template>

<script>
import TypeIt from 'typeit';

export default {
  name: "MyPosition",
  mounted () {
    new TypeIt(this.$el, {
      loop: true
    })
      .pause(1800)
      .type('I\'m studnet')
      .delete(3, {delay: 100})
      .pause(100)
      .type('ent at ', {delay: 100})
      .type('<span class="text-thammasat"><b>Thammasat</b></span>')
      .type(' <span class="text-university"><b>University</b></span>', {delay: 100})
      .pause(1500)
      .go()
    ;
  }
}
</script>
