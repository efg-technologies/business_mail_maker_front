<template>
  <main>
    <nav class="navbar navbar-dark">
      <a
        class="navbar-brand"
        href="#">
        <img
          src="~/assets/logo.png"
          height="32">
      </a>
    </nav>

    <h2>
      ビジネスメールを<br>
      楽にしよう
    </h2>

    <p>以下のフォームに入力すると、<br>
      ビジネスメール向けの文章に変換します。</p>

    <section class="container">
      <div class="row">
        <div class="col">
          <button
            type="button"
            class="btn btn-outline-primary"
            @click="f1">
            例文1
          </button>
          <button
            type="button"
            class="btn btn-outline-primary"
            @click="f2">
            例文2
          </button>
          <button
            type="button"
            class="btn btn-outline-primary"
            @click="f3">
            例文3
          </button>
          <button
            type="button"
            class="btn btn-outline-primary"
            @click="f4">
            例文4
          </button>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <textarea
            id="exampleFormControlTextarea1"
            v-model="row_text"
            class="form-control"
            rows="3"
            placeholder="変換したい文章をここに入れてください。"/>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <button
            class="btn btn-primary"
            type="submit"
            @click="translate">丁寧文へ変換</button>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <textarea
            id="exampleFormControlTextarea1"
            v-model="translate_text"
            class="form-control"
            rows="3"
            placeholder="変換された文章がここに出力されます。"/>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      row_text: '',
      translate_text: '',
      dict: {
        'ごめんなさい。この前は迷惑かけちゃいました。許してください。':
          '申し訳ありませんでした。先日はご迷惑をおかけしました。お許しください。'
      }
    }
  },
  mounted() {
    axios
      .get('https://www.goodfind.jp/')
      .then(function(response) {
        // handle success
        console.log(response)
      })
      .catch(function(error) {
        // handle error
        console.log(error)
      })
      .then(function() {
        // always executed
      })
  },
  methods: {
    f1() {
      this.row_text =
        'ごめんなさい。この前は迷惑かけちゃいました。許してください。'
    },
    f2() {
      this.row_text =
        'この間はありがとうございます。とてもおいしかったです。また連れてってください。'
    },
    f3() {
      this.row_text =
        'この前の商談ではお世話になりました。良い取引ができたと思います。またお願いします。'
    },
    f4() {
      this.row_text =
        '書類を送ります。この前の会議で提案したものです。よろしくお願いします。'
    },
    translate() {
      this.translate_text = this.dict[this.row_text]
      if (!this.translate_text) {
        // TODO: サンプル以外なのでAPIを叩く
      }
    }
  }
}
</script>

<style scoped src="./index.css">
</style>
