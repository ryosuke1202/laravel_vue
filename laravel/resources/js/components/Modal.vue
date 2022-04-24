<template>
	<div>
		<button @click="openModal">削除する</button>
		<div id="modal" v-if="isOpen">
			<div id="modal__box">
				<span id="modal__message">本当に投稿しますか?</span>
				<div id="modal__action">
					<div id="modal__btn" class="not" @click="closeModal">キャンセル</div>
					<div id="modal__btn" class="suc">投稿する</div>
				</div>
			</div>
		</div>
	</div>
</template>
MDbootstrapをつかていた関係でうまく表示されなかったのでclass指定をid指定にしてうまくいった
<script>
export default {
	data() {
      return {
        isOpen: false,
      }
    },
	methods: {
		openModal(){
			this.isOpen = true
		},
		closeModal() {
			this.isOpen = false
		}
	},
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

#modal {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.5);
	z-index: 10;
}

#modal__box {
	position: absolute;
	top: 50%;
	left: 50%;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	width: 500px;
	height: 200px;
	padding: 32px;
	background-color: #fff;
	border-radius: 4px;
	transform: translate(-50%, -50%);
}

#modal__message {
	font-size: 24px;
	text-align: center;
}

#modal__action {
	display: flex;
	justify-content: flex-end;
	margin: 0 auto;
}

#modal__btn {
	width: 130px;
	margin-left: 16px;
	padding: 8px;
	line-height: 1.5;
	font-weight: bold;
	border: 1px solid rgb(196, 196, 196);
	cursor: pointer;
	text-align: center;
}

.not {
	background-color: #999999;
	color: #fff;
}

.suc {
	color: #fff;
	border: none;
	background-color: rgb(60, 140, 245);
}
</style>