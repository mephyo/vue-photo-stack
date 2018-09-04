<template>
    <div class="photo-stack" :style="photoStackStyle">
        <photo-stack-item v-for="(cover, index) in arrangedCovers" :key="index" :src="cover" :size="size" :deviation="deviation"></photo-stack-item>
        <div class="photo-stack-name">{{title}}</div>
    </div>
</template>

<script>
    import PhotoStackItem from './PhotoStackItem.vue'
    export default {
        name: 'PhotoStack',
        components: {
            PhotoStackItem
        },
        props: {
            covers: {
                type: Array,
                required: true
            },
            title: {
                type: String,
            },
            shuffle: {
                type: Boolean,
            },
            size: {
                type: Number,
                default: 120
            },
            deviation: {
                type: Number,
                default: 30
            }
        },
        computed: {
            photoStackStyle() {
                const height = this.title ? this.size + 20 : this.size
                return {
                    width: this.size + 40 + 'px',
                    height: height + 40 + 'px'
                }
            },
            arrangedCovers() {
                if (this.shuffle) {
                    return this.shuffleCovers(this.covers)
                } else {
                    return this.covers
                }
            }
        },
        methods: {
            shuffleCovers(array) {
                for (let i = array.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [array[i], array[j]] = [array[j], array[i]];
                }
                return array;
            }
        }
    }
</script>

<style scoped>
    .photo-stack {
        position: relative;
        overflow: hidden;
    }

    .photo-stack .photo-stack-name {
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        font-size: 14px;
        font-weight: 500;
        height: 20px;
        line-height: 20px;
        text-decoration: none;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        text-align: center;
        color: #fff;
        text-shadow: 0 1px 4px rgba(0, 0, 0, 0.5);
    }
</style>