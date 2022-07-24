<script setup>

</script>

<template>
    <footer>
        <p>Challenge by <a data-replace="Frontend Mentor" href="https://www.frontendmentor.io?ref=challenge" target="_blank"><span>Frontend Mentor</span></a>.</p>
        <p>Coded by <a data-replace="Mehdi Tadjer" href="https://github.com/MehdiT-dev" target="_blank">Mehdi Tadjer</a>.</p>
    </footer>    
</template>

<style lang="scss" scoped>
footer {
    padding: 10px;
    background: $white;
    border-top: 1px solid $grayish-blue;
    text-align: center;
    color: $grayish-blue;

    p {
        margin: 5px 0;
    }
    a {
        position: relative;
        display: inline-block;
        vertical-align: top;
        overflow: hidden;
        font-weight: 700;
        color: $dark-grayish-blue;
        text-decoration: none;
        transition: transform .40s ease-in-out;
    

        &::before {
            content: '';
            position: absolute;
            display: block;
            top: 0;
            left: 0;
            height: 100%;
            width: 100%;
            background: $white;
            transform: translateY(-200%);
            transition: transform .10s ease-in-out;
        }
        &:hover::before,
        &:focus::before {
            transform: translateY(0);
        }
        &::after {
            content: attr(data-replace);
            position: absolute;
            display: block;
            top: 0;
            left: 0;
            width: 100%;
            color: $orange;
            transform-origin: 100% 50%;
            transform: translate3d(200%, 0, 0);
            transition: transform .15s ease-in-out;
        }
        &:hover::after,
        &:focus::after {
            transform: translate3d(0, 0, 0);
        }
    }
}
</style>