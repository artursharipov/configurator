<template>
    <button class="check-button">
        <svg width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><polyline fill="none" stroke="#000" stroke-width="1.1" points="4,10 8,15 17,4"></polyline></svg>
    </button>
</template>

<script>

export default {
    name: 'CheckButton',
    props: {
        // color: String
    }
}

</script>

<style scoped>
.check-button{
    color: #fff;
    display: inline-block;
    width: 40px;
    padding: 6px 4px 8px;
    text-align: center;
    cursor: pointer;
    margin-bottom: 7px;
    border-radius: 0;
    outline: 0;
    border: unset;
    margin-right: 5px;
}
.check-button svg{
    transform: scale(0);
    transition: transform .1s;

}
.check-button.active svg{
    transform: scale(1);
}
.check-button.active svg polyline{
    stroke: #fff;
    stroke-width: 1.5;
}
.red{
    background-color: #af1826;
}
.blue{
    background-color: #003fb7;
}
.darkgray{
    background-color: #646967;
}
.white{
    background-color: #ebebeb;
}
.white.active svg polyline{
    stroke: #000;
}

</style>