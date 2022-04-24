<template>
  <div>
    <button
      type="button"
      class="btn m-0 p-1 shadow-none"
    >
      <i class="fas fa-heart mr-1"
        :class="{'red-text':this.isLikedBy, 'animated heartBeat fast':this.gotToLike}"
        @click="clickLike" 
      />
      <!-- @clickは、v-on:clickの省略形です。 -->
    </button>
    {{ countLikes }}
  </div>
</template>

<script>
  export default {
    props: {
      initialIsLikedBy: {
        type: Boolean,
        default: false,
      },
      initialCountLikes: {
        type: Number,
        default: 0,
      },
      authorized: {
        type: Boolean,
        default: false,
      },
      endpoint: {
        type: String,
      },
    },
    data() {
      return {
        isLikedBy: this.initialIsLikedBy,
        countLikes: this.initialCountLikes,
        gotToLike: false,
      }
    },
    methods: {
      clickLike() {
        if (!this.authorized) {
          alert('いいね機能はログイン中のみ使用できます')
          return
        }

        this.isLikedBy
          ? this.unlike()
          : this.like()
      },
      async like() {
        const response = await axios.put(this.endpoint)

        this.isLikedBy = true
        this.countLikes = response.data.countLikes
        this.gotToLike = true
      },
      async unlike() {
        const response = await axios.delete(this.endpoint)

        this.isLikedBy = false
        this.countLikes = response.data.countLikes
        this.gotToLike = false
      },
    },
  }
</script>

likeメソッドの定義時、その手前にasyncを付けています。

またlikeメソッドの内部では、awaitが使われています。

asyncとawaitは、JavaScriptで非同期処理を簡潔に書くための仕組みです。

asyncとawaitについて聞いたことが無いという人は以下の記事を参考にしてください。

async/await入門 - async/awaitとは | CodeGrid
axios.put(this.endpoint)では、endopoint、つまりURIarticles/{article}/likeに対して、HTTPのPUTメソッドでリクエストします。

axiosはHTTP通信を行うためのJavaScriptのライブラリです。

Laravelでは、標準でこのaxiosが使用できるようになっています。

HTTP通信を行った後は、isLikedByにtrueを代入しています。この結果、ハートアイコンは赤くなります。

responseには、axiosによるHTTP通信の結果が代入されていますが、response.dataとすることでレスポンスのボディ部にアクセスできます。

レスポンスのボディ部には、Laravel側のlikeアクションメソッドの戻り値が代入されていますので、response.data.countLikesとすることで、いいね数を取得しています。

このいいね数を、VueコンポーネントのデータcountLikesに代入することで、いいね数の表示が変更されます。