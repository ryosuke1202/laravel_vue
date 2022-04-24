<template>
    <div class="card-body">
        <div class="card-text">
            <a href="" class="text-muted">
            {{ following }} フォロー
            </a>
            <a href="" class="text-muted">
            {{ follower }} フォロワー
            </a>
        </div>
    </div>
</template>

<script>
  export default {
    props: {
      followings: {
        type: Number,
      },
      followers: {
        type: Number,
      },
    },
    data() {
      return {
        countFollowings: this.followings,
        countFollowers: this.followers,
      }
    },
    computed: {
      following() {
        return this.countFollowings
      },
      follower() {
        return this.countFollowers
      },
    },
    
}

</script>