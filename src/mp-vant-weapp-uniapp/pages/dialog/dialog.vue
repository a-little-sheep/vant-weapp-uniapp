<template>
	<div class="app">
		<wrap title="提示弹窗">
			<van-cell title="提示弹窗" is-link @click="onClickAlert" />
			<van-cell title="提示弹窗(无标题)" is-link @click="onClickAlert2" />
		</wrap>

		<wrap title="确认弹窗"><van-cell title="确认弹窗" is-link @click="onClickConfirm" /></wrap>
		<wrap title="圆角按钮样式">
			<van-cell title="提示弹窗" is-link @click="onClickAlertC" />
			<van-cell title="提示弹窗(无标题)" is-link @click="onClickAlertC2" />
		</wrap>
		<wrap title="异步关闭"><van-cell title="异步关闭" is-link @click="onClickConfirmAsync" /></wrap>

		<wrap title="组件调用"><van-cell title="组件调用" is-link @click="showCustomDialog" /></wrap>

		<van-dialog
			:use-slot="true"
			title="标题"
			:async-close="true"
			:show="show"
			:show-cancel-button="true"
			@close="onClose"
			confirm-button-open-type="getUserInfo"
			@getuserinfo="getUserInfo"
		>
			<van-field :value="username" label="用户名" placeholder="请输入用户名" />
			<van-field :value="password" type="password" label="密码" :border="false" placeholder="请输入密码" />
			<image src="https://img.yzcdn.cn/vant/apple-3.jpg" />
		</van-dialog>
		<view class="clear-blank"></view>
		<van-dialog id="van-dialog" />
	</div>
</template>

<script>
import Page from '../../common/page';
const message = '代码是写出来给人看的，附带能在机器上运行';
import wrap from '@/components/wrap';
import Dialog from '@/wxcomponents/vant/dialog/dialog';
export default {
	components: {
		wrap
	},
	data() {
		return {
			show: false,
			username: '',
			password: ''
		};
	},
	methods: {
		showCustomDialog() {
			this.show = true;
		},

		onClickAlert() {
			Dialog.alert({
				title: '标题',
				message
			}).then(() => {
				console.log('confirm');
			});
		},
		onClickAlert2() {
			Dialog.alert({
				message
			}).then(() => {
				console.log('confirm');
			});
		},

		onClickAlertC() {
			Dialog.alert({
				title: '标题',
				theme: 'round-button',
				message
			}).then(() => {
				console.log('confirm');
			});
		},
		onClickAlertC2() {
			Dialog.alert({
				theme: 'round-button',
				message
			}).then(() => {
				console.log('confirm');
			});
		},

		getUserInfo(event) {
			console.log(event.detail);
		},

		onClickConfirm() {
			Dialog.confirm({
				title: '标题',
				message
			})
				.then(() => {
					console.log('confirm');
				})
				.catch(() => {
					console.log('cancel');
				});
		},
		onClickConfirmAsync() {
			Dialog.confirm({
				title: '标题',
				message: '弹窗内容',
				asyncClose: true
			})
				.then(() => {
					setTimeout(() => {
						Dialog.close();
					}, 1000);
				})
				.catch(() => {
					Dialog.close();
				});
		},

		onClose(event) {
			if (event.detail === 'confirm') {
				setTimeout(() => {
					this.show = false;
				}, 1000);
			} else {
				this.show = false;
			}
		}
	}
};
</script>

<style>
.van-button {
	margin: 5px;
}
</style>
