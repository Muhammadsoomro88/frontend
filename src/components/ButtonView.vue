<template>
  <div>
    <button :class="[showEmployees?'btn-danger':'btn-primary', 'btn']" @click="isClicked">{{ text }}</button>
  </div>
</template>

<script>
export default {
    props: ['text','showEmployees'],
    methods:{
        isClicked(){
            this.$emit('btn-clicked')
        }
    }
}
</script>

<style>
</style>