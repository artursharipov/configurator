<template>
    <button class="switch-button">
        <slot />
    </button>
</template>

<script>

export default {
    name: "SwitchButton",
    props: {

    }
}

</script>

<style scoped>

.switch-button{
    padding: 10px 20px 8px;
    background-color: unset;
    color: #9b9b9b;
    border: 1px dashed #9b9b9b;
    outline: unset;
    margin-right: 5px;
    cursor: pointer;
    font-weight: bold;
    text-transform: uppercase;
    margin-bottom: 5px;
}

.switch-button.active{
    border-color: #e9a31b;
    background-color: #e9a31b;
    color: #fff;
}

</style>