<template>
    <div>
        <section class="memory-cards">
                <card v-for="(number, index) in numbers" :key="index" 
                    v-bind:number="number"
                    v-bind:pickedCards="noMatch"
                    v-bind:index="index"
                    v-on:flipped-card="addCard"/>
        </section>
        <overlay v-if="won"/>
    </div>
</template>

<script>
import Card from './components/card';
import Overlay from './components/overlay'

export default {
    components: {
        Card,
        Overlay
    },
    data: function() {
        return {
            numbers: [1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8, 8],
            pickedCards: [],
            pickedAllCards: 0,
            won: false,
            noMatch: [],
        }
    },
    methods: {
        resetAnimation: function() {
            this.noMatch.push(this.pickedCards[0]);
            this.noMatch.push(this.pickedCards[1]);
        },
        resetCards: function() {
            this.pickedCards = [];
        },
        hasWon: function() {
            if (this.pickedAllCards === 8) {
                setTimeout(()=> {
                    this.won = true;
                }, 1000);
            }
        },
        checkMatch: function() {
            this.noMatch = [];
            if (this.pickedCards[0].number === this.pickedCards[1].number) {
                this.pickedAllCards++;
                this.hasWon();
                this.resetCards();
            } else {
                setTimeout(() => {
                    this.resetAnimation();
                    this.resetCards();
                }, 1000);
            }
        },
        addCard: function(card) {
            this.pickedCards.push(card);
            
            if(this.pickedCards.length === 2) {
                this.checkMatch();
            }
        },
        shuffle: function() {
            this.numbers = this.numbers.sort(() => Math.random() - 0.5);
        }
    }
}
</script>

<style>
    * {
        box-sizing: border-box;
    }

    body {
        height: 100vh;
        margin: 0;
    }

    div {
        position: relative;
        display: flex;
    }

    .memory-cards {
        max-width: 1000px;
        display: flex;
        flex-wrap: wrap;
        margin: auto;
        justify-content: center;
    }
</style>