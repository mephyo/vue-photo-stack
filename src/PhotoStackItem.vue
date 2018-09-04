<template>
    <img class="photo-stack-item" :src="src" @load="imageReady" ref="photoBox" :style="photoStackItemStyle" />
</template>

<script>
    export default {
        name: 'PhotoStackItem',
        props: {
            src: String,
            size: Number,
            deviation: Number
        },
        data() {
            return {
                photoStackItemStyle: {
                    maxWidth: '120px',
                    maxHeight: '120px',
                    top: '80px',
                    left: '80px',
                    marginTop: '0px',
                    marginLeft: '0px',
                    transform: 'rotate(0deg) translateZ(0)',
                    opacity: 0
                }
            }
        },
        methods: {
            calcPosition() {
                const photoBox = this.$refs.photoBox
                this.photoStackItemStyle.marginTop = photoBox.offsetHeight / -2 + 'px'
                this.photoStackItemStyle.marginLeft = photoBox.offsetWidth / -2 + 'px'
            },
            calcAngle() {
                const deviation = this.deviation ? 30 : this.deviation
                const angle = Math.floor(Math.random() * deviation) - (deviation / 2)
                this.photoStackItemStyle.transform = 'rotate(' + angle + 'deg) translateZ(0)'
            },
            calcSize() {
                if (this.size) {
                    this.photoStackItemStyle.maxWidth = this.size + 'px'
                    this.photoStackItemStyle.maxHeight = this.size + 'px'
                    this.photoStackItemStyle.top = (this.size + 40) / 2 + 'px'
                    this.photoStackItemStyle.left = (this.size + 40) / 2 + 'px'
                }
            },
            imageReady() {
                this.calcPosition()
                this.calcAngle()
                this.calcSize()
                this.photoStackItemStyle.opacity = 1
            }
        },
        watch: {
            size() {
                this.calcSize()
            },
            deviation() {
                this.calcAngle()
            }
        }
    }
</script>

<style scoped>
    .photo-stack-item {
        position: absolute;
        display: block;
        border: 2px solid #fff;
        box-shadow: 0 0 1px 2px rgba(0, 0, 0, 0.05), 0 4px 2px 2px rgba(0, 0, 0, 0.025);
        transform-origin: center;
        transition: opacity .5s;
    }
</style>