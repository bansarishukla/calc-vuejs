<template>
  <div>
    <div class="btn" @click="onClick(val)">{{val}}</div>
  </div>
</template>

<script>
export default {
  props:['val'],
  data () {

  },
  methods: {
    onClick (val) {
      this.$emit('append', val)
    }
  }
}
</script>

<style>
  .btn {
    border: 5px solid white;
    padding: 10px;
    font-weight: bold;
  }
</style>
