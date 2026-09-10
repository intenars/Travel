<template>
	<!-- 遮罩层，使用 @touchmove.stop.prevent 阻止底层页面滚动穿透 -->
	<view class="modal-mask" v-if="visible" @touchmove.stop.prevent="preventTouchMove">
		<view class="modal-container">

			<!-- 弹窗主体，相对定位以便内部元素做绝对定位 -->
			<view class="modal-content">

				<!-- 标题区 -->
				<view class="modal-header">
					<image class="warning-icon" src="/static/index/icon1.png">️</image>
					<text class="title-text">血糖偏低风险预警</text>
				</view>

				<!-- 警报描述 -->
				<view class="modal-desc">
					监测发现 <text class="highlight-name">{{ targetName }}</text>血糖偏低! <text class="highlight-name"></text>，老年人低血糖症状隐蔽，请立刻关注老人状态。
				</view>

				<!-- 处置建议列表 -->
				<view class="advice-list">
					<view class="advice-item">
						<view class="bullet-icon"></view>
						<text class="advice-text">立即让老人停止活动，就地休息，及时补充糖分，观察老人是否心慌，出冷汗，头晕</text>
					</view>

					<view class="advice-item">
						<view class="bullet-icon"></view>
						<text class="advice-text">若出现意识恍惚，浑身无力，嗜睡，立即拨打120，做好应急处置。</text>
					</view>
				</view>

				<!-- 底部操作区 -->
			<view class="modal-footer">
				<button class="action-btn" @click="handleCheck">立即查看</button>
			</view>

				<!-- 右下角吉祥物图片 - 点击触发语音播报，动态浮动动画 -->
			<image class="mascot-img" src="/static/index/mascot_water_sad.png" mode="aspectFit" @click="speakAlarm"></image>

			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "RiskWarningModal",
		props: {
			// 控制弹窗显隐
			visible: {
				type: Boolean,
				default: false
			},
			// 预警对象姓名
			targetName: {
				type: String,
				default: '张爷爷'
			}
		},
		data() {
			return {}
		},
		watch: {
			visible: {
				immediate: true,
				handler(val) {
					// 弹窗显示时自动语音播报，关闭时停止
					if (val) {
						setTimeout(() => this.speakAlarm(), 300);
					} else {
						this.stopSpeak();
					}
				}
			}
		},
		methods: {
			preventTouchMove() {
				return false;
			},
			handleCheck() {
				this.$emit('check');
				this.$emit('update:visible', false);
				// 跳转到血糖恢复方案页面
				// uni.navigateTo({ url: '/pages/sugar/sugar' });
			},
			// 报警内容语音播报（Web Speech API，H5可用）
			speakAlarm() {
				const text = `监测发现${this.targetName}血糖偏低，实时血糖三点六毫摩尔每升。老年人低血糖易突发摔倒，请立刻让老人坐下休息并补充糖分。`;
				const w = (typeof window !== 'undefined') ? window : null;
				// 兼容老 WebView 的 webkit 前缀
				const synth = w && (w.speechSynthesis || w.webkitSpeechSynthesis);
				const UCtor = w && (w.SpeechSynthesisUtterance || w.webkitSpeechSynthesisUtterance);
				if (!w || !synth || !UCtor) {
					uni.showToast({
						title: '不支持语音播报(synth:' + (!!synth) + '/U:' + (!!UCtor) + ')',
						icon: 'none',
						duration: 2500
					});
					return;
				}
				const doSpeak = () => {
					synth.cancel();
					const u = new UCtor(text);
					u.lang = 'zh-CN';
					u.rate = 0.95;
					u.pitch = 1;
					u.onstart = () => {
						uni.showToast({ title: '正在播报警报', icon: 'none', duration: 1200 });
					};
					u.onerror = (ev) => {
						if (ev && ev.error && ev.error !== 'canceled' && ev.error !== 'interrupted') {
							uni.showToast({ title: '语音播报失败：' + ev.error, icon: 'none', duration: 1500 });
						}
					};
					synth.speak(u);
				};
				// H5 首次 voices 可能未就绪，等 voiceschanged 再播
				if (typeof synth.getVoices === 'function' && synth.getVoices().length === 0) {
					let done = false;
					const fire = () => {
						if (done) return;
						done = true;
						doSpeak();
					};
					synth.onvoiceschanged = fire;
					setTimeout(fire, 300); // 兜底，避免事件不触发
				} else {
					doSpeak();
				}
			},
			stopSpeak() {
				if (typeof window !== 'undefined' && window.speechSynthesis) {
					window.speechSynthesis.cancel();
				}
			}
		},
		beforeDestroy() {
			this.stopSpeak();
		}
	};
</script>

<style lang="scss" scoped>
	.modal-mask {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: rgba(0, 0, 0, 0.6);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 999;
	}

	.modal-container {
		width: 620rpx;
		position: relative;
	}

	.modal-content {
		background: linear-gradient(180deg, #FFF5F5 0%, #FFFFFF 15%, #FFFFFF 100%);
		border-radius: 40rpx;
		padding: 50rpx 40rpx 40rpx;
		box-shadow: 0 8rpx 40rpx rgba(230, 53, 53, 0.2);
		border: 2rpx solid rgba(255, 220, 220, 0.6);
		position: relative;
		/* 不设 overflow:hidden，让右下角吉祥物完整溢出显示且可点击 */
	}

	.modal-header {
		display: flex;
		align-items: center;
		margin-bottom: 24rpx;

		.warning-icon {
			width: 32rpx;
			height: 32rpx;
			margin-right: 12rpx;
		}

		.title-text {
			font-size: 38rpx;
			font-weight: 800;
			color: #171717;
		}
	}

	.modal-desc {
		font-size: 30rpx;
		color: #333333;
		line-height: 1.6;
		margin-bottom: 36rpx;

		.highlight-name {
			color: #E86737;
			font-weight: bold;
			margin: 0 4rpx;
		}
	}

	.advice-list {
		margin-bottom: 40rpx;

		.advice-item {
			display: flex;
			align-items: flex-start;
			margin-bottom: 24rpx;

			&:last-child {
				margin-bottom: 0;
			}

			.bullet-icon {
				width: 8rpx;
				height: 28rpx;
				background: linear-gradient(180deg, #E63535 0%, #FF6B6B 100%);
				border-radius: 6rpx;
				margin-right: 16rpx;
				margin-top: 10rpx;
				flex-shrink: 0;
			}

			.advice-text {
				font-size: 28rpx;
				color: #333333;
				line-height: 1.6;
				flex: 1;
			}
		}
	}

	.modal-footer {
		display: flex;
		justify-content: flex-start;

		.action-btn {
			width: 260rpx;
			height: 84rpx;
			line-height: 84rpx;
			margin: 0;
			background: linear-gradient(90deg, #FF6F22 0%, #FF3D00 100%);
			color: #FFFFFF;
			font-size: 32rpx;
			font-weight: bold;
			border-radius: 42rpx;
			box-shadow: 0 8rpx 20rpx rgba(255, 61, 0, 0.3);
			border: none;

			&::after {
				border: none;
			}
		}
	}

	/* 右下角吉祥物 - 动态浮动动画 */
	.mascot-img {
		position: absolute;
		right: -30rpx;
		bottom: -100rpx;
		width: 260rpx;
		height: 280rpx;
		z-index: 100;
		display: block;
		animation: mascotFloat 2.6s ease-in-out infinite;
	}

	@keyframes mascotFloat {
		0% {
			transform: translateY(0) rotate(-3deg);
		}

		50% {
			transform: translateY(-22rpx) rotate(3deg);
		}

		100% {
			transform: translateY(0) rotate(-3deg);
		}
	}
</style>
