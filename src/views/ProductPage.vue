<script setup>

import { ref, onMounted } from 'vue';
// Importation des composants
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import Lightbox from '@/components/Lightbox.vue';
import IconCart from '../components/icons/IconCart.vue';
// Import des composables
// import { useCart } from '@/composables/useCart'

// Déclaration du produit
const product = {
    brand: 'Sneaker Company',
    model: 'Fall limited edition sneakers',
    description: "These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they'll withstand everything the weather can offer.",
    pictures: [
        '@/assets/images/image-product-1.jpg',
        '@/assets/images/image-product-2.jpg',
        '@/assets/images/image-product-3.jpg',
        '@/assets/images/image-product-4.jpg'
    ],
    thumbnails: [
        '@/assets/images/image-product-1-thumbnail.jpg',
        '@/assets/images/image-product-2-thumbnail.jpg',
        '@/assets/images/image-product-3-thumbnail.jpg',
        '@/assets/images/image-product-4-thumbnail.jpg'
    ],
    startingPrice: 250.00,
    isOnSale: true,
    promotionPercentage: 50,
}

// Règle le problème d'affichage d'images dynamiquement
for (let i=0; i<product.pictures.length; i++) {
    product.pictures[i] = require(`@/assets/images/image-product-${i+1}.jpg`);
    product.thumbnails[i] = require(`@/assets/images/image-product-${i+1}-thumbnail.jpg`);
}

// Défilement des images du slider
let pictureIndex = ref(0);
let timeout = ref(null);
const thumbnails = ref([]);

onMounted(() => {
    thumbnails.value[pictureIndex.value].parentElement.classList.add('active');
});
const showPrevImage = () => {
    if (timeout.value === true) {
        return;
    } else {
        timeout.value = true;
        setTimeout(() => {
            timeout.value = false;
            if (pictureIndex.value == 0) {
                pictureIndex.value = product.pictures.length-1;
            } else {
                pictureIndex.value--;
            }
        }, 50);
    }
}
const showNextImage = () => {
    if (timeout.value === true) {
        return;
    } else {
        timeout.value = true;
        setTimeout(() => {
            timeout.value = false;
            if (pictureIndex.value == product.pictures.length-1) {
                pictureIndex.value = 0;
            } else {
                pictureIndex.value++;
            }
        }, 50);
    }
}
const displaySelectedImg = (e) => {
    thumbnails.value[pictureIndex.value].parentElement.classList.remove('active');
    pictureIndex.value = Number(e.target.dataset.pictureNb);
    e.target.parentElement.classList.add('active');
}

// Choix du nombre d'articles / Ajout au panier
let nbProduct = ref(0);
const decreaseNbProduct = () => {
    if (nbProduct.value === 0) return;
    nbProduct.value = nbProduct.value -= 1;
}
const increaseNbProduct = () => {
    if (nbProduct.value >= 10) return;
    nbProduct.value = nbProduct.value += 1;
}
const addToCart = (e) => {
    console.log(e);
    if (nbProduct.value === 0) {
        console.log('Sélectionner la quantité à ajouter.');
        return;
    } else {
        console.log(`Vous avez ajouté ${nbProduct.value} ${product.model} à votre panier.`);
        nbProduct.value = 0;
    }
}

// Gestion lightbox
let lightboxDisplayed = ref(false);
const displayLightbox = () => {
    if (document.body.clientWidth > 1180) {
        lightboxDisplayed.value = !lightboxDisplayed.value;
    }
    console.log(lightboxDisplayed.value);
}
</script>

<template>
    <Header/>
    <div id="container">
        <div class="product-view">
            <div class="slider">
                <span @click="showPrevImage" class="prev">
                    <img src="@/assets/images/icon-previous.svg" alt="">
                </span>
                <span @click="showNextImage" class="next">
                    <img src="@/assets/images/icon-next.svg" alt="">
                </span>
                <div class="picture">
                    <img @click="displayLightbox" :src="product.pictures[pictureIndex]" alt="">
                </div>
            </div>
            <div class="thumbnails">
                <div v-for="(thumbnail, index) in product.thumbnails" class="thumbnail" :key="index">
                    <img @click="displaySelectedImg" :data-picture-nb="index" :src="thumbnail" ref="thumbnails" alt="">
                </div>
            </div>
        </div>
        <div class="product-description">
            <h2 class="brand">{{ product.brand }}</h2>
            <h1 class="model">{{ product.model }}</h1>
            <p class="description">{{ product.description }}</p>
            <div v-if="product.isOnSale" class="sale-price">
                <p class="price">${{ (( product.startingPrice * product.promotionPercentage ) / 100).toFixed(2) }}<span class="promo">{{ product.promotionPercentage }}%</span></p>
                
                <p class="previous-price">${{ product.startingPrice.toFixed(2) }}</p>
            </div>
            <div v-else class="starting-price">
                <p class="price">${{ product.startingPrice.toFixed(2) }}</p>
            </div>
            <div class="input-container">
                <div class="input-box">
                    <img @click="decreaseNbProduct" class="minus" src="@/assets/images/icon-minus.svg" alt="">
                    <img @click="increaseNbProduct" class="plus" src="@/assets/images/icon-plus.svg" alt="">
                    <input type="number" disabled :value="nbProduct">
                </div>
                <a @click="addToCart" class="btn">
                    <IconCart class="btn-icon"/>
                    <span>Add to cart</span>
                </a>
            </div>
        </div>
    </div>
    <Footer/>
    <Lightbox 
    @close-lightbox="displayLightbox"
    :thumbnails="product.thumbnails"
    :pictures="product.pictures"
    :lightboxDisplayed="lightboxDisplayed"
    :pictureIndex="pictureIndex"
    />
</template>

<style lang="scss" scoped>
#container {
    @include respond('large') {
        max-width: 1116px;
        margin: 0 auto;
        display: flex;
        justify-content: space-around;
        min-height: calc(100vh - 200px);

        .product-view,
        .product-description {
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        .product-view {
            flex-basis: 40%;
            align-items: center;
            
            .slider {
                height: auto;
                width: 100%;
                aspect-ratio: 1/1;
                border-radius: 15px;
                overflow: hidden;
                margin: 15px;

                .picture {
                    cursor: pointer;
                }
                span {
                    display: none;
                }
            }
            .thumbnails {
                display: flex;
                justify-content: space-between;
                width: 99%;
                height: 88px;
                margin: 15px;

                .thumbnail {
                    width: 88px;
                    border-radius: 15px;
                    aspect-ratio: 1/1;
                    cursor: pointer;

                    &.active {
                        outline: 2px solid $orange;

                        img {
                            opacity: .25;
                        }
                    }

                    img {
                        width: auto;
                        height: 100%;
                        border-radius: 15px;

                        &:hover {
                            // filter: saturate(80%)
                            opacity: .5;
                        }
                    }
                }
            }
        }
        .product-description {
            display: flex;
            flex-basis: 43%;
            
            h2 {
                font-size: 0.85em;
            }
            h1 {
                font-size: 2.8em;
                margin-bottom: 32px;
            }
            > p {
                font-size: 1.09em;
            }
            .sale-price {
                flex-direction: column;
                align-items: flex-start;
                margin: 10px 0 25px;

                p {
                    margin-bottom: 10px;
                }
            }
            .input-container {
                display: flex;
                justify-content: space-between;

                .input-box {
                    flex-basis: 36%;

                    input {
                        font-size: 1.1em;
                    }
                    img {

                        &.minus {
                            left: 0px;
                        }
                        &.plus {
                            right: 0px;
                        }
                    }
                }
                a.btn {
                    flex-basis: 61%;
                }
            }
        }
    }
}
.product-view {
    position: relative;
    overflow: hidden;;
    .slider {
        display: flex;
        height: 300px;
        width: 100%;

        span {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            height: 40px;
            width: 40px;
            background: $white;
            border-radius: 50%;
            cursor: pointer;

            img {
                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                width: 25%;
            }

            &.prev {
                left: 20px;
            }
            &.next {
                right: 20px;
            }
        }
        div {
            height: 100%;
            display: flex;
            align-items: center;
            overflow: hidden;
            img {
                width: 100%;
                max-width: 100vw;
                height: auto;
            }
        }
    }
    .thumbnails {
        display: none;
    }
}
.product-description {
    padding: 20px;

    > * {
        margin-bottom: 15px;
    }
    h1 {
        text-transform: capitalize;
        font-size: 1.8em;
    }
    h2 {
        color: $orange;
        text-transform: uppercase;
        font-size: 0.8em;
        letter-spacing: 0.15em;
    }
    > p {
        color: $dark-grayish-blue;
        line-height: 1.6em;
    }
    .sale-price {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin: 25px 0;

        p {
            &.price {
                position: relative;
                font-weight: 700;
                font-size: 1.8em;

                span.promo {
                    position: absolute;
                    right: -65px;
                    top: 50%;
                    transform: translateY(-50%);
                    font-size: 0.6em;
                    font-weight: 700;
                    padding: 3px 8px;
                    border-radius: 5px;
                    background: $pale-orange;
                    color: $orange;
                }
            }
            &.previous-price {
                font-weight: 700;
                color: $grayish-blue;
                text-decoration: line-through;
            }
        }
    }
}
// Remove arrows from input type number for Chrome, Safari, Edge, Opera
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}
.input-box {
    position: relative;
    height: 55px;

    img {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        padding: 15px;
        cursor: pointer;

        &.minus {
            left: 10px;
        }
        &.plus {
            right: 10px;
        }
    }
    input[type=number] {
        border: none;
        border-radius: 10px;
        background: $light-grayish-blue;
        width: 100%;
        height: 100%;
        text-align: center;
        font-family: 'Kumbh Sans', sans-serif;
        font-weight: 700;
        -moz-appearance: textfield; // Remove arrows from input type number for Firefox
    }
}
a.btn {
    display: block;
    height: 55px;
    width: 100%;
    border-radius: 10px;
    background: $orange;
    text-align: center;
    font-weight: 700;
    line-height: 55px;
    color: $white;
    cursor: pointer;

    svg, span {
        margin: 0 7px;
        font-size: 1.1em;
    }
}
</style>