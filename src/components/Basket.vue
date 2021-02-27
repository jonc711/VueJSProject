<template>
  <div>
  <h3> Menu: </h3>
    <ul>
      <li v-for="a in itemBasket" v-bind:key="a">
        {{ a[0] }} x{{a[1]}}
      </li>
      
    </ul>
    <button v-on:click='findTotal'> Calculate Price </button>
    <p v-show='showed'> Subtotal: ${{ subtotal }} </p>
    <p v-show='showed'> Total: ${{ total }} </p>
    

  </div>
</template>

<script>
export default {
  name: 'Basket',
  props: {
    itemBasket: {
      type: Array
    }
  },

  data: function () {
      return {
        showed: false,
        subtotal: 0,
        
      }
    
  },

  methods: {
    findTotal: function () {
      var i;
      var currTotal = 0;
      for (i=0; i < this.itemBasket.length; i++) {
        currTotal += this.itemBasket[i][2];
      }
      this.subtotal = currTotal;
      this.showed = true;

    }
  },

  computed: {
    total: function() {
      var num = this.subtotal * 1.07;
      return num.toFixed(2);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
