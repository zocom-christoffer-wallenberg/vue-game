<template>
  <article class="memory-card" v-bind:class="{ 'flip': flip }" v-on:click="flipCard">
        <span class="front">{{ number }}</span>
        <span class="back">Memory</span>
  </article>
</template>

<script>
export default {
    name: 'card',
    props: {
        number: Number,
        pickedCards: Array,
        index: Number
    },
    data: function() {
        return {
            flip: false,
        }
    },
    watch: {
        pickedCards: function() {
            for(let i = 0;i < this.pickedCards.length;i++) {
                if (this.pickedCards[i].index === this.index) {
                    this.flip = false;
                }
            }
        }
    },
    methods: {
        flipCard: function() {
            this.flip = true;
            this.$emit('flipped-card', { number: this.number, index: this.index });
        }
    }
}
</script>

<style>
    .memory-card {
        width: 200px;
        height: 200px;
        background: #692D55;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: #ffffff;
        box-shadow: 2px 2px 5px #000000;
        position: relative;
        transition: transform 0.8s;
        transform-style: preserve-3d;
        margin: 0.5rem;
    }

    .front, .back {
        position: absolute;
        backface-visibility: hidden;
        font-size: 1.5em;
        padding: 20px;
    }

    .flip{
        transform: rotateY(180deg);
    }

    .front {
        transform: rotateY(180deg);
    }

</style>