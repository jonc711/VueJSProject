<template>
  <div>

  <button v-on:click="add"> + </button><p> {{counter}} </p><button v-on:click="sub"> - </button>
  </div>
</template>

<script>

export default {
  data: function () {
    return {
      counter : 0
    }
  },
  props: {
    item: {
      type: Object
    }
  },
  methods: {
    add: function () {
      if (this.counter == 10) {
        alert("You cannot purchase more than 10 items");
      } else {
        this.counter += 1;
      }
      this.$emit('counter', this.item, this.counter);
    },

    sub: function () {
      if (this.counter == 0) {
        alert("Cannot be negative");
      } else {
        this.counter -= 1;
      }
      this.$emit('counter', this.item, this.counter);
    }

  }
  
}
</script>

<style>

</style>
