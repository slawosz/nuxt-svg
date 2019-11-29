<template>
  <no-ssr>
    <g>
      <polygon :points="points"></polygon>

      <circle cx="100" cy="100" r="80"></circle>

      <Label
        v-for="(stat, index) in stats"
        :stat="stat"
        :index="index"
        :total="stats.length">
      </Label>
    </g>
  </no-ssr>
</template>

<script>
import Label from '~/components/Label.vue'

// math helper...
function valueToPoint (value, index, total) {
  var x     = 0
  var y     = -value * 0.8
  var angle = Math.PI * 2 / total * index
  var cos   = Math.cos(angle)
  var sin   = Math.sin(angle)
  var tx    = x * cos - y * sin + 100
  var ty    = x * sin + y * cos + 100
  return {
    x: tx,
    y: ty
  }
}

export default {
  name: 'Polygraph',
  props: {
    stats: Array
  },
  computed: {
    // a computed property for the polygon's points
    points: function () {
      var total = this.stats.length
      return this.stats.map(function (stat, i) {
        var point = valueToPoint(stat.value, i, total)
        return point.x + ',' + point.y
      }).join(' ')
    }
  },
  components: { Label }
}
</script>

<style>
</style>
