<script setup>
import { ref } from 'vue';

const sideNav = ref();

const toggleSideNav = function() {
    sideNav.value.classList.toggle('open');
    // console.log(sideNav.value);
}

</script>

<template>
    <header role="banner">
        <div ref="sideNav" id="side-nav">
            <p id="close-btn" @click="toggleSideNav">
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
            <p id="open-btn" @click="toggleSideNav">
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
        width: 250px;
        height: 100vh;
        background: $white;
        padding: 25px;
        transform: translateX(-250px);
        transition: transform .5s ease;
        z-index: 50;

        &.open {
            transform: translateX(0);
        }

        p {
            padding-bottom: 5px;
            width: 20px;
            cursor: pointer;
        }
        nav {
            margin-top: 50px;

            ul li {
                list-style-type: none;
                margin: 23px 0;

                a {
                    text-decoration: none;
                }
            }
        }
    }
    #primary-nav {
        display: flex;
        align-items: center;
        
        p {
            cursor: pointer;
        }
        #desktop-menu {
            display: none;
        }
    }
    #secondary-nav {
        justify-self: right;
        height: 20px;
    
        p {
            display: inline-block;
            cursor: pointer;
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