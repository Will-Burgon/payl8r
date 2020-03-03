<template>
  <div class="retailer">
    <img :src="logo" alt="name">
    <p><nuxt-link :to="{name: 'retailer-name', params: {name: name.toLowerCase().replace(/ /g, '_'), industry: industry}}">{{name}}</nuxt-link></p>
    <small><nuxt-link :to="{name: 'retailer-industry', params: {name: name.toLowerCase().replace(/ /g, '_'), industry: industry}}">{{industry}}</nuxt-link></small>
  </div>
</template>

<script>
export default {
props: {
  name: String,
  logo: String,
  industry: String
}
}
</script>

<style lang="scss">
.retailer {
  border-radius: 10px 0 10px 0;
  text-align: center;
  box-shadow: 10px 10px 18px -10px rgba(0,0,0,0.2);
  padding: 1.5rem;
  img {
    width: 100%;
  }
  p {
    a {
      background: var(--color-accent);
      color: var(--color-grey);
      display: inline-block;
      padding: .75rem 0.25rem;
      width: 150px;
      clip-path: polygon(20% 0, 100% 0%, 80% 90%, 0% 100%);
      transition: 0.4s;
      &:hover {
      clip-path: polygon(0 0, 100% 0%, 100% 100%, 0% 100%);
      }
    }
  }
  small {
    text-transform: uppercase;
    border-bottom: 2px solid var(--color-black);
     a {
       color: var(--color-grey-dark);
     }
  }
}
</style>
