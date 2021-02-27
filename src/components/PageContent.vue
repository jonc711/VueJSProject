<template>
  <div>
    <ul>
  <li v-for="b in itemPage" :key="b.id">
    <h1>{{ b.name }}</h1> 
    <img :src="b.imageURL">
    <p> ${{b.price}} </p>
    <QuantityCounter v-bind:item = 'b' v-on:counter="onCounter"></QuantityCounter>
  </li>
  
  
</ul>
<Basket v-bind:itemBasket = 'itemsSelected'></Basket>
</div>
  
</template>

<script>
import QuantityCounter from './QuantityCounter.vue'
import Basket from './Basket.vue'
export default {
  components: {
    QuantityCounter,
    Basket,
  },
  props: {
    itemPage: {
      type: Array
    }
  },

  data: function () {
    return {
      itemsSelected: [],
    }
  },

  methods: {
    onCounter: function (item, count) {
      if (this.itemsSelected.length === 0 && count > 0) {
        //If there is nothing in items selected, push the ORDER in
        this.itemsSelected.push([item.name, count, item.price]);
      } else {
        var checker = false;
        // Loop through everything to check what is not in the basket
        for (let i = 0; i < this.itemsSelected.length; i++) {
          const curr_item = this.itemsSelected[i];
          const item_name = curr_item[0];

          if (item.name == item_name && count > 0) {
            this.$set(this.itemsSelected[i], 1, count);
            checker = true;
          } else if (item_name == item.name && count == 0) {
            this.itemsSelected.splice(i,1);
            checker = true;
          }
        }
      if (checker == false) {
            this.itemsSelected.push([item.name, count, item.price]);
          } 

        }
      }
  
    },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#itemsList {
  width: 100%;
  max-width: 70%;
  margin: 0px;
  padding: 0 5px;
  box-sizing: border-box;
}
ul {
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  padding: 0;
}
li {
  flex-grow: 1;
  flex-basis: 300px;
  text-align: center;
  padding: 10px;
  border: 1px solid #222;
  margin: 10px;
}
img {
  width: 135px;
  height: 135px;
}

#price {
  font-size: 30px;
}

#itemName {
  font-size: 30px;
}

#shoppingBasket {
  position: absolute;
  top: 23%;
  left: 78%;
}
</style>
