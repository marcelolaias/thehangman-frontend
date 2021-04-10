<template>
    <div class="gallows">
      <img class="gallows-img" :src="require(`../assets/${errors}.svg`)" />
    </div>
</template>

<script>
export default ({
    name: 'Gallows',
    props: {
      errors: Number
    },
    data() {
        return {
            
        }
    },
    methods: {

    }
})
</script>