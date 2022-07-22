<script setup>
//import {  } from 'vue';
</script>

<template>
    <header role="banner">
        <div id="side-nav">
            <p id="close-btn" @click="closeSideNav">
                <img src="@/assets/images/icon-close.svg" alt="">
            </p>
            <nav>
                <ul>
                    <li><a href="">Collections</a></li>
                    <li><a href="">Men</a></li>
                    <li><a href="">Women</a></li>
                    <li><a href="">About</a></li>
                    <li><a href="">Contact</a></li>
                </ul>
            </nav>
        </div>
        <div id="primary-nav">
            <p id="open-btn" @click="openSideNav">
                <img src="@/assets/images/icon-menu.svg" alt="">
            </p>
            <p class="logo">
                <img src="@/assets/images/logo.svg" alt="">
            </p>
            <nav id="desktop-menu">
                <ul>
                    <li><a href="">Collections</a></li>
                    <li><a href="">Men</a></li>
                    <li><a href="">Women</a></li>
                    <li><a href="">About</a></li>
                    <li><a href="">Contact</a></li>
                </ul>
            </nav>
        </div>
        <div id="secondary-nav">
            <p @click="openCart">
                <img src="@/assets/images/icon-cart.svg" alt="">
            </p>
            <p @click="openProfile">
                <img src="@/assets/images/image-avatar.png" alt="">
            </p>
        </div>
    </header>    
</template>

<style lang="scss" scoped>
header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: $white;
    height: 70px;
    padding: 25px;
    border: 1px solid $black;

    #side-nav {
        position: absolute;
        top: 0;
        left: 0;
        width: 200px;
        height: 100vh;
        transform: translateX(-200px);
    }
    #primary-nav {
        display: flex;
        align-items: center;
        
        #desktop-menu {
            display: none;
        }
    }
    #secondary-nav {
        justify-self: right;
        height: 20px;
    
        p {
            display: inline-block;
            margin: 0 10px;
    
            &:last-child {
                height: 20px;
                margin-right: 0;
                img {
                height: 100%;
                }
            }
        }
    }
    p {
        &.logo {
            margin: 0 15px;
        }
    }
}
</style>