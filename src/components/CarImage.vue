<template>

    <img :src="src">

</template>

<script>

export default {
    name: 'CarImage',
    props: {
        src: {
            type: String 
        }
    }

}

</script>