<template>
  <section class="overlay" v-bind:class="{ 'show': !close }">
        <a href="#" class="close" v-on:click="closeOverlay">X</a>
        <h1>You won!</h1>
  </section>
</template>

<script>
export default {
    name: 'overlay',
    props: {
        showOverlay: Boolean
    },
    data: function() {
        return {
            close: this.showOverlay
        }
    },
    /*watch: {
        showOverlay: function() {
            this.close = this.showOverlay;
        }
    },*/
    methods: {
        closeOverlay: function() {
            this.close = true;
        }
    }
}
</script>

<style>
    .overlay {
        position: absolute;
        background: rgba(0, 0, 0, 0.8);
        width: 100%;
        height: 100%;
        display: none;
        align-items: center;
        justify-content: center;
    }

    .overlay h1 {
        font-size: 48px;
        color: #ffffff;
    }

    .overlay .close {
        position: absolute;
        top: 0;
        right: 0;
        margin: 4rem;
        color: #ffffff;
        text-decoration: none;
        font-size: 32px;
    }

    .show {
        display: flex;
    }
</style>