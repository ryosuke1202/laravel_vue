<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <div class="card mt-3">
          <div class="card-body pt-0">
            <div class="card-text">
              <form method="POST" :action="url">
                <div class="md-form">
                <label>タイトル</label>
                <input type="text" name="title" class="form-control" required>
                </div>
                <div class="form-group">
                <label></label>
                <textarea name="body" required class="form-control" rows="16" placeholder="本文"></textarea>
                </div>
                <button type="button" class="btn blue-gradient btn-block" @click="openModal">投稿する</button>
                <div id="modal" v-if="isOpen" @close="showContent = false">
                    <div id="modal__box">
                        <span id="modal__message">本当に投稿しますか?</span>
                        <div id="modal__action">
                            <div id="modal__btn" class="not" @click="closeModal">キャンセル</div>
                            <div id="modal__btn" class="suc" type="submit">投稿する</div>
                        </div>
                    </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      url: {
        type: String,
      },
    },
    data() {
      return {
        isOpen: false,
      }
    },
    methods: {
      openModal () {
          this.isOpen = true
      },
      closeModal () {
          this.isOpen = false
      }
    },
  }
</script>