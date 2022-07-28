<script setup>
import { ref } from 'vue';

const sideNav = ref();

const toggleSideNav = function() {
    sideNav.value.classList.toggle('open');
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
        <div id="side-nav-bg"></div>
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
        position: fixed;
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
        
            + #side-nav-bg {
                display: block;
            }
        }
        + #side-nav-bg {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            height: 100vh;
            width: 100vw;
            background: rgba(0, 0, 0, 0.5);
            transition: transform .5s ease;
            z-index: 10;
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
            margin-right: 15px;
            
            &.logo {
            }
        }
        #desktop-menu {
            display: none;
        }
    }
    #secondary-nav {
        // justify-self: right;
        display: flex;
        align-items: center;
        height: 20px;
    
        p {
            display: inline-block;
            cursor: pointer;
            margin: 0 10px;
    
            &:last-child {
                height: 100%;
                margin-right: 0;
                img {
                    height: 100%;
                    border-radius: 50%;
                }
            }
        }
    }

    @include respond ('large') {
        max-width: 1116px;
        margin: 0 auto;
        height: 115px;
        padding: 0;
        border: none;
        border-bottom: 1px solid $grayish-blue;

        #primary-nav {
            height: 100%;
            #open-btn {
                display: none;
            }
            p.logo {
                margin-right: 50px;
            }
            #desktop-menu {
                display: block;
                height: 100%;
                line-height: 115px;

                ul {
                    height: 100%;

                    li {
                        position: relative;
                        display: inline-block;
                        margin-right: 35px;

                        &::before {
                            content: '';
                            position: absolute;
                            display: block;
                            bottom: 0;
                            left: 0;
                            width: 100%;
                            height: 0;
                            border-radius: 5px;
                            background: $orange;
                        }
                        &:hover {
                            a {
                                color: $very-vark-blue;
                            }

                            &::before {
                                height: 5px;
                            }
                        }
                        
                        a {
                            display: inline-block;
                            text-decoration: none;
                            color: $dark-grayish-blue;
                            font-weight: 400;
                        }
                    }
                }
            }
        }
        #secondary-nav {
            height: 50px;
            p:last-child {
                margin-left: 30px;

                img:hover{
                    outline: 3px solid $orange;
                }
            }
        }
    }
}
</style>