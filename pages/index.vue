<template>
  <div>
    <Toggle @changedInput="ChangedInput"/>

    <div class="retailers__grid" v-if="toggle">

        <div v-for="(retailer, i) in nameArray" :key="i">
          <Retailer
            :name="retailer.name"
            :logo="retailer.logo"
            :industry="retailer.industry"
           />
        </div>

    </div>
     <div class="retailers__false" v-else>

        <div v-for="(industry) in industries" :key="industry" >
          <h3>{{industry}}</h3>
          <div class="retailers__grid">
          <div  v-for="(retailer) in filteredArray(industry)" :key="retailer.name" class="retailers__row">
            <Retailer
            :name="retailer.name"
            :logo="retailer.logo"
            :industry="retailer.industry"
           />
          </div>
          </div>
        </div>

    </div>

  </div>
</template>

<script>
import data from '~/assets/retailer-list.json';
import Retailer from '~/components/Retailer'
import Toggle from '~/components/Switch'
export default {
asyncData(){
const retailers  = data;
return {
  retailers
  }
},
data(){
  return {
    toggle: true,
    industries: []
  }
},
components: {
  Retailer,
  Toggle
},
computed: {
    nameArray() {
    const compare = (a, b) => {
      if(this.toggle){
      if (a.name < b.name)
        return -1;
      if (a.name > b.name)
        return 1;
      return 0;
    }
     }
    return this.retailers.sort(compare);
  },

},
mounted () {
    this.industries =new Set(this.retailers.map(company => company.industry))
},
methods: {
  ChangedInput(e) {
    this.toggle = e
  },
  filteredArray(key) {
    const filter = this.retailers.filter(retailer => retailer.industry === key);
    return filter
  }
}
}
</script>

<style lang="scss">
  .retailers {
    &__grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      grid-gap: 40px;
        @media screen and (max-width: 768px) {
       grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      }
    }
    &__row {
     margin: 1rem 0;
    }
    &__false {
      text-align: center;
      h3 {
        text-transform: uppercase;
        color: var(--color-grey-dark);
        display: inline-block;
        text-align: center;
        padding: 0.5rem 1rem;
        position: relative;
         @media screen and (max-width: 768px ) {
            border-bottom: 2px solid var(--color-black);
           }
        &::after, &::before {
          content: "";
          position: absolute;
          width: 150px;
          height: 4px;
          background: var(--color-black);
          transform: translateY(-50%);
           top: 50%;
           @media screen and (max-width: 768px ) {
            display: none
           }
        }
        &::after {
          left: 100%;
        }
        &::before {
          right: 100%;
        }
      }
    }
  }
</style>
