<template>
    <div class="image-list">
        <div class="columns has-text-centered">
            <div class="column">
                <p class="image-container" v-for="(img, idx) in even_images" :key="idx">
                    <img :src="img.src" :alt="img.title" @click="insertImage(img)">
                </p>
            </div>
            <div class="column">
                <p class="image-container" v-for="(img, idx) in odd_images" :key="idx">
                    <img :src="img.src" :alt="img.title" @click="insertImage(img)">
                </p>
            </div>
        </div>
        <div v-if="lone_image" class="columns is-centered has-text-centered">
            <div class="column is-half">
                <p class="image-container">
                    <img :src="lone_image.src" :alt="lone_image.title" @click="insertImage(img)">
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    computed: {
        odd_images() {
            return this.images.filter((img, idx) => idx % 2 !== 0)
        },
        even_images() {
            if (this.images.length % 2 !== 0) {
                return this.images
                    .filter((img, idx) => idx % 2 === 0)
                    .slice(0, -1)
            } else {
                return this.images.filter((img, idx) => idx % 2 === 0)
            }
        },
        lone_image() {
            if (this.images.length % 2 !== 0) {
                return this.images[this.images.length - 1]
            } else {
                return false
            }
        }
    },
    data() {
        return {
            images: [
                {
                    title: 'A cat',
                    src: 'https://i.ytimg.com/vi/7OD55d6iRCQ/maxresdefault.jpg'
                },
                {
                    title: 'Another Cat',
                    src:
                        'https://images.pexels.com/photos/45201/kitty-cat-kitten-pet-45201.jpeg?auto=compress&cs=tinysrgb&h=350'
                },
                {
                    title: 'A third cat',
                    src:
                        'https://images.pexels.com/photos/104827/cat-pet-animal-domestic-104827.jpeg?auto=compress&cs=tinysrgb&h=350'
                }
            ]
        }
    },
    methods: {
        insertImage(img) {
            this.$emit('insert-image', img)
        }
    }
}
</script>

<style scoped>
.image-list img {
    height: 128px;
    cursor: pointer;
}
.image-container {
    background: whitesmoke;
    width: 100%;
}
.image-container:hover {
    transform: scale(1.05);
    transition: 0.3s;
}
</style>
