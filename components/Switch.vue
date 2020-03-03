<template>
  <div class="switch">
    <p>Name</p>
    <label class="switch__label">
      <input type="checkbox" @change="getInput" />
      <span class="switch__slider"></span>
    </label>
   <p> Industry</p>
  </div>
</template>

<script>
export default {
data(){
  return {
    switch: true
  }
},
methods: {
  getInput() {
    this.switch = !this.switch;
    this.$emit('changedInput', this.switch)
  }
}
}
</script>

<style lang="scss">
  .switch {
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 2rem;
    & > * {
      margin: 0 .8rem;
    }
    &__label {
       position: relative;
       display: inline-block;
       width: 60px;
       height: 34px;
       & input {
          opacity: 0;
          width: 0;
          height: 0;

       }
    }
    &__slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #ccc;
      -webkit-transition: .4s;
      transition: .4s;
      &::before {
        position: absolute;
        content: "";
        height: 26px;
        width: 26px;
        left: 4px;
        bottom: 4px;
        background-color: white;
        -webkit-transition: .4s;
        transition: .4s;
      }
    }
  }
   .switch__label input:checked + .switch__slider {
      background-color: var(--color-accent);
    }
   .switch__label input:focus + .switch__slider {
      box-shadow: 0 0 1px var(--color-accent);
    }
   .switch__label input:checked + .switch__slider::before {
      transform: translateX(26px);
    }
</style>
