<template>
  <div>
    <div class="btn" @click="onClick(val)">{{val}}</div>
  </div>
</template>

<script>
export default {
  props:['val'],
  data () {
    return {

    }
  },
  methods: {
    onClick (val) {
      this.$emit('append', val)
    }
  }
}
</script>

<style>
  /* .btn {
      border: 1px solid black ;
    font-weight: bold;
  } */
</style>
