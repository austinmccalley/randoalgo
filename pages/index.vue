<template>
  <div class="">
    <div class="container">
      <div>
        <logo />
        <transition name="fade" mode="out-in">
          <div class="noAlgo">
            <Intro v-if="!isHidden" />
            <div v-if="!isHidden" class="buttons">
              <b-button @click="gen" size="lg" class="generate" variant="outline-primary">
                Generate
              </b-button>
            </div>
          </div>
        </transition>
        <div v-if="isHidden" class="Algo">
          <h2 class="algoName">
            {{ algosName }}
          </h2>
          <b-button @click="gen" size="lg" class="generate" variant="outline-primary">
            Generate Another!
          </b-button>
        </div>
      </div>
      <div class="push" />
    </div>
    <Footer />
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Footer from '~/components/Footer.vue'
import Intro from '~/components/Intro.vue'

import algosFile from '~/static/algos.json'

export default {
  head: {
    titleTemplates: '%s - RandoAlgo',
    meta: [{
      charset: 'utf-8'
    },
    {
      name: 'viewport',
      content: 'width=device-width, initial-scale=1'
    },
    { hid: 'description', name: 'description', content: 'Meta description' }

    ]
  },
  components: {
    Logo,
    Intro,
    Footer
  },
  data () {
    return {
      isHidden: false,
      algosName: '',
      algos: algosFile
    }
  },
  mounted () {
    if (process.browser) {
      this.$gtag('config', 'UA-156469206-1', {
        page_title: this.$meta.title,
        page_path: this.$route.fullPath
      })
    }
  },
  methods: {
    gen (e) {
      const r = Math.floor(Math.random() * Object.keys(this.algos).length) + 1
      const algo = this.algos[r].name
      this.algosName = algo
      this.isHidden = true
    }
  }
}

</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    margin-bottom: -50px;
  }

  .Algo {
    padding-top: 10px;
  }

  .algoName {
    padding: 2.5%;
  }

  .buttons {
    font-family: 'Roboto Condensed', sans-serif;
    padding-top: 15px;
    padding-bottom: 10%;
  }

  .generate {
    border-color: #59b3d3;
    outline: none;
    color: #59b3d3;
  }

  .generate:hover {
    color: #ffffff;
    background-color: #59b3d3;
    border-color: #59b3d3;
  }

  .fade-enter-active,
  fade-leave-active {
    transition: opacity 1.0s;
  }

  .fade-enter,
  .face-leave-to {
    opacity: 0;
  }

  .footer,
  .push {
    font-family: 'Roboto Condensed', sans-serif;
    font-weight: 300;
    font-style: italic;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 5px;

    height: 50px;
    margin: 0 auto;
    padding: 1%;
  }

  .footer {
    background-color: #efefef;
  }

</style>
