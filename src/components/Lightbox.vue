<script setup>
import { ref, onUpdated, watch, defineProps } from 'vue';

// !!!
// Assigner la valeur d'une prop à une valeur réactive lui fera perdre sa réactivité !!!
// !!!

// => Assigner un watcher sur la prop lightboxDisplayed ?
// Clean le code + comments

let lbPictureIndex = ref(0);
let picturesArray = ref([])
let lbThumbnails = ref([]);

const props = defineProps({
    lightboxDisplayed: {
        type: Boolean,
        required: true
    },
    lightboxImgUrl: {
        type: String,
        required: true
    },
    pictures: {
        type: Array,
        required: true
    },
    thumbnails: {
        type: Array,
        required: true
    },
    pictureIndex: {
        type: Number,
        requried: true
    },
});
picturesArray = props.pictures;
let currentImage = ref(picturesArray[lbPictureIndex.value]);

onUpdated(() => {
    currentImage = props.pictures[lbPictureIndex.value];
});

// Gestion de l'image à afficher en grand
const displaySelectedImg = (e) => {
    lbPictureIndex.value = Number(e.target.dataset.pictureNb);
    // console.log(lbPictureIndex.value)
    currentImage = props.pictures[lbPictureIndex.value];
    // console.log(currentImage)
}

// Gestion des boutons précédents et suivants
const displayPrevImg = () => {
    lbPictureIndex.value === 0 ? lbPictureIndex.value = props.pictures.length-1 : lbPictureIndex.value--;
}
const displayNextImg = () => {
    lbPictureIndex.value === props.pictures.length-1 ? lbPictureIndex.value = 0 : lbPictureIndex.value++;
}

// Gestion des thumbnails (active / !active)
watch(lbPictureIndex, (currentValue, oldValue) => {
    console.log(oldValue, '=>', currentValue);
    lbThumbnails.value[oldValue].parentElement.classList.remove('active');
    lbThumbnails.value[currentValue].parentElement.classList.add('active');
});
watch(props.lightboxDisplayed, (currentValue, oldValue)  => {
    console.log(oldValue, '=>', currentValue);
    console.log(lbPictureIndex.value);
});
</script>

<template>
    <div v-if="lightboxDisplayed" class="lightbox">
        <div class="lightbox-container">
            <button @click="$emit('closeLightbox')" class="lightbox-close">Close</button>
            <div class="lightbox-img">
                <img :src="props.pictures[lbPictureIndex]" alt="">
                <button @click="displayPrevImg" class="lightbox-prev">Précédent</button>
                <button @click="displayNextImg" class="lightbox-next">Suivant</button>
            </div>
            <div class="lightbox-thumbnails">
                <div v-for="(thumbnail, index) in thumbnails" :key="index" class="thumbnail">
                    <img @click="displaySelectedImg" :data-picture-nb="index" :src="thumbnail" alt="" ref="lbThumbnails">
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .lightbox {
        position: fixed;
        display: flex;
        align-items: center;
        justify-content: center;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.90);
        z-index: 99;

        .lightbox-container {
            // position: absolute;
            // top: 50%;
            // left: 50%;
            // transform: translate(-50%, -50%);
            // height: 80vh;
            width: 550px;
            text-align: right;

            button {
                border: none;
                color: transparent;
                cursor: pointer;
            }
            .lightbox-close {
                width: 25px;
                height: 25px;
                margin-bottom: 30px;
                background: 
                    transparent
                    url(@/assets/images/icon-close.svg) center center / 100% 100% no-repeat;
            }
            .lightbox-img {
                position: relative;
                margin-bottom: 25px;
            
                img {
                    width: 100%;
                    height: auto;
                    border-radius: 15px;
                }
                .lightbox-prev,
                .lightbox-next {
                    width: 55px;
                    height: 55px;
                    border-radius: 50%;
                    position: absolute;
                    top: 50%;
                    transform: translateY(-50%);
                }
                .lightbox-prev {
                    background: $white
                    url(@/assets/images/icon-previous.svg) 40% center / 20% 35% no-repeat;
                    left: -25px;
                }
                .lightbox-next {
                    background: $white
                    url(@/assets/images/icon-next.svg) 60% center / 20% 35% no-repeat;
                    right: -25px;
                }
            }
            .lightbox-thumbnails {
                display: flex;
                justify-content: center;

                .thumbnail {
                    background: $white;
                    width: 88px;
                    height: 88px;
                    margin: 15px;
                    border-radius: 15px;

                    &.active {
                        outline: 3px solid $orange;

                        img {
                            opacity: .25;
                        }
                    }
                }
                img {
                    height: 100%;
                    width: 100%;
                    border-radius: 15px;
                    cursor: pointer;

                    &:hover {
                        opacity: .5;
                    }
                }
            }
        }
    }
</style>

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