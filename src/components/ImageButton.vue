<template>
    <button class="image-button">
        <img :src="src">
    </button>
</template>

<script>

export default {
    name: 'ImageButton',
    props: {
        src: String
    }
}

</script>

<style scoped>
.image-button{
    color: #fff;
    display: inline-block;
    padding: 6px 4px 8px;
    text-align: center;
    cursor: pointer;
    margin-bottom: 7px;
    border-radius: 0;
    outline: 0;
    border: unset;
    margin-right: 5px;
    width: 75px;
    background-color: unset;
    border: 1px dashed transparent;
}
.image-button.active{
    border-color: #e9a31b;
}
.image-button img{
    width: 100%;
}

</style>