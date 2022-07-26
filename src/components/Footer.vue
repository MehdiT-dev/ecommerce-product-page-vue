<script setup>

</script>

<template>
    <footer>
        <p>Challenge by <a data-replace="Frontend Mentor" href="https://www.frontendmentor.io?ref=challenge" target="_blank"><span>Frontend Mentor</span></a>.</p>
        <p>Coded by <a data-replace="Mehdi Tadjer" href="https://github.com/MehdiT-dev" target="_blank"><span>Mehdi Tadjer</span></a>.</p>
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
        transition: transform 1.40s ease-in-out;
    
        span {
            display: inline-block;
            transition: all .3s ease;
        }
        &:hover span {
            transform: translateX(-200px);
        }
        &::before {
            content: '';
            position: absolute;
            // display: block;
            bottom: 0;
            left: 0;
            height: 2px;
            width: 100%;
            background: $orange;
            transform: scaleX(0);
            transform-origin: left;
            transition: transform .3s ease-in-out .3s;
        }
        &:hover::before {
            transform: scaleX(1);
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
            transform: translateX(200%);
            transition: transform .3s ease-in-out;
        }
        &:hover::after,
        &:focus::after {
            transform: translateX(0);
        }
    }
}
</style>