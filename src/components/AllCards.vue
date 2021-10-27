<template>
  <div>

    <select class="select select-price" v-model="selectSort">
        <option v-for="rule in sortRules" :key="rule.key" :value="rule.key">{{ rule.title }}</option>
    </select>

    <select class="select select-category" v-model="selectCategory">
      <option value="0">Все категории</option>
      <option v-for="category in materalList" :key="category.id" :value="category.id" selected>{{ category.name }}</option>
    </select>

    <div class="block">
        <div v-for="item in filteredProducts" :key="item.id" is="Card" :item="item">
        </div>
    </div>

  </div>
</template>

<script>
import _ from 'lodash';
import Card from './Card.vue'
export default {
  name: "AllCards",
  components: {
    Card
  },
  data() {
    return {
      itemsDataList: [],
      materalList: [],
      sortRules: [
            { key :'price.current_price:asc', title: 'Цена по возрастанию' },
            { key :'price.current_price:desc', title: 'Цена по убыванию' }
        ],
      selectCategory: 0,
      selected: 'test',
      selectSort: 'price.current_price:asc'
    };
  },
  created() {
    this.getDataList()
  },
  computed: {
    filteredProducts() {
      if(this.selectCategory) {
        return this.itemsDataList.filter(product => {
            return this.selectCategory == 0 || product.material == this.selectCategory;
        })
      }
      let sorted = _.sortBy(this.itemsDataList, product => {
        return Number(product.price.current_price);
      });

      if (this.sortDir === 'desc') {
          sorted = sorted.reverse();
      }
        return sorted;
      },
      sortDir: function() {
        return this.selectSort.split(':')[1];
    },
  },
  methods: {
    getDataList() {
        Promise.all([
            fetch("./data/items.json"),
            fetch("./data/materials.json")
        ]).then(function (responses) {
            return Promise.all(responses.map(function (response) {
                return response.json();
            }));
        }).then(data => (
            this.itemsDataList = data[0],
            this.materalList = data[1]
        ))
        .catch(function (error) {
            console.log(error);
        });
    },
  },
};
</script>

<style lang="scss">

.select {
    width: 28.8rem;
    height: 4rem;
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    border: none;
    background-image: url('../assets/arrow_icon.svg');
    background-repeat: no-repeat;
    background-position: center right 1.5rem;
    background-color: #F2F2F2;
    margin-right: 2.4rem;
    margin-bottom: 4.1rem;
    padding-left: 1.6rem;
    font-style: normal;
    font-weight: normal;
    font-size: 1.4rem;
    line-height: 150%;
    letter-spacing: 0.03em;
    color: #000000;
    outline: none;

    @media (max-width: 1024px) {
     width: 48%;
     margin-right: 0;
     &-price {
       margin-right: 2.4rem;
     }
    }

    @media (max-width: 767px) {
      width: 100%;

      &-price {
       margin-right: 0;
     }

    }
}

.block {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    flex-wrap: wrap;

    @media (max-width: 1024px) {
        justify-content: space-between;
    }

    div {
       width: 23%;
       height: auto;
       border: 1px solid #EEEEEE;
       border-radius: .5rem;
       margin-bottom: 2rem;
       margin-right: 3.5rem;
       &:nth-child(4n) {
         margin-right: 0;
       }

       @media (max-width: 1700px) {
         margin-right: 2rem;
       }

       @media (max-width: 1024px) {
          width: 48%;
          margin-right: 0;
       }

       @media (max-width: 767px) {
          width: 100%;
          margin: 0 0 2rem 0;
       }
    }
}

</style>