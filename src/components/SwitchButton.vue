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

<style>

.switch-button{
    padding: 8px 14px;
    background-color: unset;
    color: #9b9b9b;
    border: 1px dashed #9b9b9b;
    outline: unset;
    margin-right: 5px;
    cursor: pointer;
}

.switch-button.active{
    border-color: #e9a31b;
    background-color: #e9a31b;
    color: #fff;
}

</style>