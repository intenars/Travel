<template>
	<view class="page-container">
		<!-- 顶部原生渐变背景 -->
		<view class="ambient-gradient-bg"></view>

		<!-- 1. 顶部 Header (包含模拟微信右上角胶囊) -->
		<view class="header-section">
			<view class="title-wrapper">
				<text class="page-title">浪无忧</text>
				<text class="page-subtitle">导游端 · 银发团智能管家</text>
			</view>
			<!-- 模拟小程序右上角原生胶囊 (仅用于视觉还原，实际开发中小程序自带) -->

		</view>

		<!-- 2. 预警中心概览 (带闪电图标) -->
		<view class="summary-panel card-shadow">
			<view class="panel-header">
				<view class="icon-lightning-wrapper">
					<!-- 纯CSS绘制闪电图标，避免引入外部图片 -->
					<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path d="M9.5 2H18.5L13 9H20.5L8.5 22L11 12.5H4L9.5 2Z" stroke="white" stroke-width="2"
							stroke-linejoin="round" />
					</svg>

				</view>
				<view class="header-text">
					<text class="h-title">预警中心</text>
					<text class="h-desc">今日 1 条待处理</text>
				</view>
			</view>

			<view class="stats-grid">
				<view class="stat-box">
					<text class="s-num color-danger">0</text>
					<text class="s-label">危急</text>
				</view>
				<view class="stat-box">
					<text class="s-num color-danger">0</text>
					<text class="s-label">高危</text>
				</view>
				<view class="stat-box">
					<text class="s-num color-warning">1</text>
					<text class="s-label">预警</text>
				</view>
				<view class="stat-box">
					<text class="s-num color-success">29</text>
					<text class="s-label">正常</text>
				</view>
			</view>
		</view>

		<!-- 3. 筛选 Tabs (药丸状) -->
		<view class="filter-tabs">
			<view class="tab-pill active">全部 1</view>
			<view class="tab-pill outline">危急/高危 0</view>
			<view class="tab-pill outline">预警 1</view>
		</view>

		<!-- 4. 预警事件列表 -->
		<view class="alert-list">

			<!-- [预警级别: 橘色] -->
			<view class="alert-card border-warning card-shadow">
				<view class="ac-header">
					<view class="ac-user-info">
						<view class="status-dot dot-warning"></view>
						<text class="ac-name">陈爷爷</text>
						<text class="ac-type">健康预警</text>
						<view class="ac-tag tag-warning">预警</view>
					</view>
					<text class="ac-time">11:00</text>
				</view>

				<!-- 心率波动曲线 74→85→76 -->
				<view class="ac-hr-chart">
					<view class="hr-title">心率波动（bpm）</view>
					<view class="hr-chart-area">
						<svg viewBox="0 0 300 80" class="hr-svg" style="overflow:visible">
							<defs>
								<linearGradient id="hrLine" x1="0" y1="0" x2="1" y2="0">
									<stop offset="0%" stop-color="#4CAF50" />
									<stop offset="50%" stop-color="#FF9500" />
									<stop offset="100%" stop-color="#FF8A3D" />
								</linearGradient>
							</defs>
							<!-- 曲线 74→85→76，下降段初始隐藏 -->
							<polyline
								class="hr-line"
								:class="{ draw: hrPhase }"
								points="0,55 80,40 150,25 200,15 250,30 300,45"
								fill="none"
								stroke="url(#hrLine)"
								stroke-width="3"
								stroke-linecap="round"
								stroke-linejoin="round" />
							<!-- 起点 74 -->
							<circle cx="0" cy="55" r="4.5" fill="#4CAF50" stroke="#fff" stroke-width="2" />
							<!-- 峰值 85 -->
							<circle cx="200" cy="15" r="5" fill="#FF9500" stroke="#fff" stroke-width="2" />
							<!-- 当前点：从峰值滑到76 -->
							<circle
								:cx="hrPhase ? 300 : 200"
								:cy="hrPhase ? 45 : 15"
								r="5"
								fill="#FF8A3D" stroke="#fff" stroke-width="2"
								class="hr-end-dot" />
						</svg>
						<!-- 数值标签 -->
						<view class="hr-num a">74</view>
						<view class="hr-num b">85</view>
						<view class="hr-num c" v-if="hrPhase">76</view>
						<!-- Y轴刻度 -->
						<view class="hr-y-axis">
							<text>90</text>
							<text>80</text>
							<text>70</text>
						</view>
						<view class="hr-x-axis">
							<text>11:00</text>
							<text>11:15</text>
							<text>11:30</text>
						</view>
					</view>
				</view>

				<view class="ac-actions">
					<button class="btn btn-warning-solid" @click="startHrAnim">立即处理</button>
					<button class="btn btn-warning-outline">通知家属</button>
				</view>

				<!-- 浪无忧吉祥物形象：动态浮动动画，点击触发语音播报 -->
				<!-- <image class="ac-mascot" src="/static/index/mascot_water_sad.png" mode="aspectFit" @click="speakAlarm"></image> -->
			</view>

		</view>

		<!-- 5. 服务台账 -->
		<view class="ledger-panel card-shadow">
			<view class="panel-top">
				<view class="pt-left">
					<view class="icon-book"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"
							xmlns="http://www.w3.org/2000/svg">
							<path
								d="M2.6665 1.99998C2.6665 1.63179 2.96498 1.33331 3.33317 1.33331H12.6665C13.0347 1.33331 13.3332 1.63179 13.3332 1.99998V14C13.3332 14.3682 13.0347 14.6666 12.6665 14.6666H3.33317C2.96498 14.6666 2.6665 14.3682 2.6665 14V1.99998Z"
								stroke="#2A2A2A" stroke-width="2" stroke-linejoin="round" />
							<path d="M5.3335 1.33331V14.6666" stroke="#2A2A2A" stroke-width="2" stroke-linecap="round"
								stroke-linejoin="round" />
							<path d="M8 4H10.6667" stroke="#FC7631" stroke-width="2" stroke-linecap="round"
								stroke-linejoin="round" />
							<path d="M8 6.66669H10.6667" stroke="#FC7631" stroke-width="2" stroke-linecap="round"
								stroke-linejoin="round" />
							<path d="M3.3335 1.33331H7.3335" stroke="#333333" stroke-width="2" stroke-linecap="round"
								stroke-linejoin="round" />
							<path d="M3.3335 14.6667H7.3335" stroke="#333333" stroke-width="2" stroke-linecap="round"
								stroke-linejoin="round" />
						</svg>
					</view>
					<text class="pt-title">服务台账</text>
				</view>
				<view class="btn-add">
					<text class="icon-plus">⊕</text> 新增
				</view>
			</view>

			<view class="ledger-list">
				<!-- 记录项 1 (已处理) -->
				<view class="ledger-item">
					<view class="li-header">
						<text class="li-title">血压异常处置记录</text>
						<text class="li-name-tag">刘奶奶</text>
						<text class="li-status tag-success">已处理</text>
					</view>
					<view class="li-content">
						09:15血压152/96，血氧95%，安排游客坐下休息，联系随行医护，暂时退出参观活动，等待进一步评估。
					</view>
					<view class="li-footer">处理人：海安</view>
				</view>

				<!-- 记录项 2 (待处理) -->
				<view class="ledger-item">
					<view class="li-header">
						<text class="li-title">血压异常处置记录</text>
						<text class="li-name-tag">刘奶奶</text>
						<text class="li-status tag-danger-light">待处理</text>
					</view>
					<view class="li-content">
						09:15血压152/96，血氧95%，安排游客坐下休息，联系随行医护，暂时退出参观活动，等待进一步评估。
					</view>
					<view class="li-action">
						<button class="btn-handle-small">立即处理</button>
					</view>
				</view>
			</view>

			<view class="expand-more">还有 2 条，点击展开</view>
		</view>

		<!-- 6. 团员名单 (底部折叠面板) -->
		<view class="team-panel card-shadow">
			<view class="tp-left">
				<view class="icon-users">

					<svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path
							d="M6.33333 6.66667C7.622 6.66667 8.66667 5.622 8.66667 4.33333C8.66667 3.04467 7.622 2 6.33333 2C5.04467 2 4 3.04467 4 4.33333C4 5.622 5.04467 6.66667 6.33333 6.66667Z"
							stroke="#FC7631" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
						<path
							d="M10.8691 2.33337C11.5467 2.74167 11.9999 3.48461 11.9999 4.33337C11.9999 5.18214 11.5467 5.92507 10.8691 6.33337"
							stroke="#2A2A2A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
						<path
							d="M1.3335 13.6V14H11.3335V13.6C11.3335 12.1066 11.3335 11.3598 11.0429 10.7894C10.7872 10.2876 10.3792 9.87967 9.87746 9.62401C9.30703 9.33337 8.5603 9.33337 7.06683 9.33337H5.60016C4.1067 9.33337 3.35996 9.33337 2.78952 9.62401C2.28776 9.87967 1.87981 10.2876 1.62415 10.7894C1.3335 11.3598 1.3335 12.1066 1.3335 13.6Z"
							stroke="#FC7631" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
						<path
							d="M14.6665 14V13.6C14.6665 12.1066 14.6665 11.3598 14.3758 10.7894C14.1202 10.2876 13.7122 9.87969 13.2104 9.62402"
							stroke="#2A2A2A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
					</svg>


				</view>
				<text class="tp-title">团员名单</text>
			</view>
			<view class="icon-arrow-down"> <svg width="16" height="16" viewBox="0 0 16 16" fill="none"
					xmlns="http://www.w3.org/2000/svg">
					<path
						d="M8.00016 14.6667C11.6821 14.6667 14.6668 11.6819 14.6668 8.00004C14.6668 4.31814 11.6821 1.33337 8.00016 1.33337C4.31826 1.33337 1.3335 4.31814 1.3335 8.00004C1.3335 11.6819 4.31826 14.6667 8.00016 14.6667Z"
						fill="#979797" stroke="#979797" stroke-width="2" stroke-linejoin="round" />
					<path d="M11 7L8 10L5 7" stroke="white" stroke-width="2" stroke-linecap="round"
						stroke-linejoin="round" />
				</svg>
			</view>
		</view>

		<!-- 底部安全留白 -->
		<view class="safe-bottom-area"></view>

		<!-- 导游弹窗预警 -->
		<view class="warn-overlay" v-if="showWarn" @click="closeWarn">
			<view class="warn-modal" @click.stop>
				<view class="wm-close" @click="closeWarn">✕</view>
				<image class="wm-mascot" src="/static/index/mascot_water_sad.png" mode="aspectFit" @click="speakAlarm"></image>
				<text class="wm-title">健康预警提示</text>
				<text class="wm-msg">导游陈爷爷心跳有点快，心率85，请及时关注</text>
				<view class="wm-btn" @click="handleView">立即查看</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				showWarn: true, // 弹窗预警
				hrPhase: false // 心率曲线动画：false=停在85峰值，true=降到76
			};
		},
		mounted() {
			// 页面加载后稍等触发语音播报
			setTimeout(() => this.speakAlarm(), 500);
		},
		beforeDestroy() {
			if (this.hrTimer) clearTimeout(this.hrTimer);
			if (typeof window !== 'undefined' && window.speechSynthesis) {
				window.speechSynthesis.cancel();
			}
		},
		methods: {
			startHrAnim() {
				// uni.showToast({ title: '已开始处理，5秒后更新', icon: 'none', duration: 1500 });
				// 点击后5秒触发曲线下降
				if (this.hrTimer) clearTimeout(this.hrTimer);
				this.hrTimer = setTimeout(() => {
					this.hrPhase = true;
				}, 5000);
			},
			// 弹窗"立即查看"：关闭弹窗 + 触发曲线5秒后下降
			handleView() {
				this.showWarn = false;
				if (typeof window !== 'undefined' && window.speechSynthesis) {
					window.speechSynthesis.cancel();
				}
				this.startHrAnim();
			},
			closeWarn() {
				this.showWarn = false;
				// 关闭弹窗时停止语音播报
				if (typeof window !== 'undefined' && window.speechSynthesis) {
					window.speechSynthesis.cancel();
				}
			},
			// 陈爷爷 心率预警语音播报
			speakAlarm() {
				const text = '导游陈爷爷心跳有点快，心率85，请及时关注。';
				const w = (typeof window !== 'undefined') ? window : null;
				const synth = w && (w.speechSynthesis || w.webkitSpeechSynthesis);
				const UCtor = w && (w.SpeechSynthesisUtterance || w.webkitSpeechSynthesisUtterance);
				if (!w || !synth || !UCtor) {
					uni.showToast({
						title: '不支持语音播报',
						icon: 'none',
						duration: 1500
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
						uni.showToast({ title: '正在播报预警', icon: 'none', duration: 1200 });
					};
					u.onerror = (ev) => {
						if (ev && ev.error && ev.error !== 'canceled' && ev.error !== 'interrupted') {
							uni.showToast({ title: '播报失败：' + ev.error, icon: 'none', duration: 1500 });
						}
					};
					synth.speak(u);
				};
				if (typeof synth.getVoices === 'function' && synth.getVoices().length === 0) {
					let done = false;
					const fire = () => {
						if (done) return;
						done = true;
						doSpeak();
					};
					synth.onvoiceschanged = fire;
					setTimeout(fire, 300);
				} else {
					doSpeak();
				}
			}
		}
	};
</script>

<style lang="scss" scoped>
	/* ================== 全局设计变量 ================== */
	$page-bg: #F7F8FA;
	$text-title: #111111;
	$text-main: #333333;
	$text-sub: #2A2A2A;
	$text-gray: #999999;

	/* 橘色/预警体系 */
	$brand-orange: #FF7043;
	$brand-orange-grad: linear-gradient(90deg, #FF834E 0%, #FF6633 100%);
	$warning-light-bg: #FFF5F0;
	$warning-border: rgba(255, 112, 67, 0.3);

	/* 红色/危急体系 */
	$color-danger: #F53F3F;
	$danger-light-bg: #FFF1F0;
	$danger-border: rgba(245, 63, 63, 0.3);

	/* 绿色/正常体系 */
	$color-success: #00B42A;
	$success-light-bg: #F6FFED;

	/* ================== 基础重置 ================== */
	.page-container {
		min-height: 100vh;
		background-color: $page-bg;
		font-family: -apple-system, BlinkMacSystemFont, "PingFang SC", "Helvetica Neue", Arial, sans-serif;
		position: relative;
		overflow-x: hidden;
		padding-bottom: 50rpx;
	}

	button::after {
		border: none;
	}

	/* 去除小程序按钮自带黑边 */

	/* 高保真阴影 */
	.card-shadow {
		box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.03);
	}

	/* 顶部环境光晕 */
	.ambient-gradient-bg {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 500rpx;
		background-image: url(/static/bg.png);
		background-size: 100% 100%;
		z-index: 0;
	}

	/* ================== 1. 顶部 Header ================== */
	.header-section {
		position: relative;
		z-index: 1;
		padding: 100rpx 32rpx 32rpx;
		/* 预留状态栏高度 */
		display: flex;
		justify-content: space-between;
		align-items: center;

		.title-wrapper {
			display: flex;
			flex-direction: column;


			.page-title {
				font-size: 48rpx;
				font-weight: bold;
				color: #111;
				line-height: 1.2;
			}

			.page-subtitle {
				font-size: 28rpx;
				font-weight: bold;
				color: #111;
				line-height: 1.2;
				margin-top: 10rpx;
			}
		}

		/* 微信胶囊 1:1 还原 */
		.wechat-capsule {
			display: flex;
			align-items: center;
			justify-content: center;
			width: 174rpx;
			height: 64rpx;
			background: rgba(255, 255, 255, 0.6);
			border: 1rpx solid rgba(0, 0, 0, 0.08);
			border-radius: 32rpx;
			backdrop-filter: blur(10px);

			.capsule-btn {
				flex: 1;
				text-align: center;
				font-size: 36rpx;
				color: #000;
				line-height: 64rpx;
				font-weight: bold;

				&.circle-target {
					font-size: 32rpx;
					font-weight: 400;
				}
			}

			.capsule-divider {
				width: 1rpx;
				height: 36rpx;
				background: rgba(0, 0, 0, 0.1);
			}
		}
	}

	/* ================== 2. 预警中心概览 ================== */
	.summary-panel {
		position: relative;
		z-index: 1;
		border-radius: 32rpx;
		margin: 12rpx 32rpx 32rpx;
		padding: 32rpx;

		background: rgba(255, 255, 255, 0.5);
		border-radius: 32rpx;
		border: 1px solid #FFFFFF;

		.panel-header {
			display: flex;
			align-items: center;
			margin-bottom: 32rpx;

			.icon-lightning-wrapper {
				width: 80rpx;
				height: 80rpx;
				background: linear-gradient(146deg, #FC7631 0%, #DD502D 100%);
				border-radius: 32rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				margin-right: 24rpx;
				box-shadow: 0 4rpx 12rpx rgba(255, 102, 51, 0.2);

				/* CSS绘制内嵌闪电 */
				.css-lightning {
					width: 14rpx;
					height: 28rpx;
					background: white;
					clip-path: polygon(100% 0, 20% 45%, 60% 45%, 0 100%, 80% 55%, 40% 55%);
				}
			}

			.header-text {
				display: flex;
				flex-direction: column;

				.h-title {
					font-size: 34rpx;
					font-weight: 600;
					color: $text-title;
				}

				.h-desc {
					font-size: 24rpx;
					color: $text-sub;
					margin-top: 6rpx;
				}
			}
		}

		.stats-grid {
			display: flex;
			justify-content: space-between;
			gap: 16rpx;

			.stat-box {
				flex: 1;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;



				width: 122rpx;
				height: 148rpx;
				background: rgba(255, 255, 255, 0.8);
				border-radius: 16px 16px 16px 16px;
				border: 1px solid #FFFFFF;

				.s-num {
					font-size: 48rpx;
					font-weight: bold;
					line-height: 1.2;
					margin-bottom: 4rpx;
				}

				.s-label {
					font-size: 24rpx;
					color: $text-main;
					font-weight: 500;
				}

				.color-danger {
					color: $color-danger;
				}

				.color-warning {
					color: $brand-orange;
				}

				.color-success {
					color: $color-success;
				}
			}
		}
	}

	/* ================== 3. 筛选 Tabs ================== */
	.filter-tabs {
		position: relative;
		z-index: 1;
		display: flex;
		align-items: center;
		margin: 32rpx 32rpx;
		justify-content: space-around;

		.tab-pill {

			font-size: 26rpx;
			font-weight: 500;

			width: 208rpx;
			height: 80rpx;
			background: #FC7631;
			border-radius: 16rpx;
			display: flex;
			align-items: center;
			justify-content: center;


			&.active {
				background: $brand-orange-grad;
				color: #FFFFFF;
				box-shadow: 0 4rpx 12rpx rgba(255, 102, 51, 0.3);

				font-family: PingFang SC, PingFang SC;
				font-weight: 500;
				font-size: 28rpx;
			}

			&.outline {
				background: #FFFFFF;
				color: $text-sub;
				border: 1rpx solid #EAEAEA;
				font-family: PingFang SC, PingFang SC;
				font-weight: 500;
				font-size: 28rpx;
			}
		}
	}

	/* ================== 4. 预警列表 ================== */
	.alert-list {
		margin: 0 32rpx;
		position: relative;
		z-index: 1;
	}

	.alert-card {
		border-radius: 32rpx;
		padding: 32rpx;
		margin-bottom: 32rpx;

		background: #F8F7F4;
		border: 1px solid #FC7631;

		position: relative;
		/* 不裁切，让右下角吉祥物完整溢出显示且可点击 */

		/* 级别色块定义 */
		&.border-warning {
			border: 2px solid #FC7631;
		}

		&.border-danger {
			border: 1rpx solid #FF383C;
		}
		/* 右下角浪无忧吉祥物：配合语音播报的动态形象 */
		.ac-mascot {
			position: absolute;
			right: -10rpx;
			bottom: -90rpx;
			width: 240rpx;
			height: 260rpx;
			z-index: 10;
			animation: mascotFloat 2.6s ease-in-out infinite;
		}

		.ac-header {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 20rpx;

			.ac-user-info {
				display: flex;
				align-items: center;

				.status-dot {
					width: 18rpx;
					height: 18rpx;
					border-radius: 50%;
					margin-right: 16rpx;
				}

				.dot-warning {
					background: $brand-orange;
				}

				.dot-danger {
					background: $color-danger;
				}

				.ac-name {
					font-size: 32rpx;
					font-weight: 600;
					color: $text-title;
					margin-right: 12rpx;
				}

				.ac-type {
					font-size: 28rpx;
					font-weight: 500;
					color: $text-title;
					margin-right: 16rpx;
				}

				.ac-tag {
					font-size: 22rpx;
					padding: 4rpx 14rpx;
					border-radius: 8rpx;
					font-weight: 500;
				}

				.tag-warning {
					color: $brand-orange;
					background: $warning-light-bg;
					border: 1rpx solid rgba(255, 112, 67, 0.2);
				}

				.tag-danger {
					color: $color-danger;
					background: $danger-light-bg;
					border: 1rpx solid rgba(245, 63, 63, 0.2);
				}
			}

			.ac-time {
				font-size: 26rpx;
				color: $text-gray;
			}
		}

		/* 心率波动曲线 */
		.ac-hr-chart {
			margin-bottom: 16rpx;
			.hr-title {
				font-size: 24rpx; font-weight: 600; color: #333;
				margin-bottom: 12rpx;
			}
			.hr-chart-area {
				position: relative; height: 180rpx;
				background: #FAFBFC; border-radius: 14rpx;
				padding: 20rpx 20rpx 36rpx;
				border: 1rpx solid #F0EDE8;
			}
			.hr-svg {
				position: absolute; left: 20rpx; right: 20rpx; top: 20rpx;
				height: calc(100% - 56rpx);
				width: calc(100% - 40rpx);
				z-index: 2;
			}
			/* 下降段描边动画：初始只显示到峰值(0~204)，处理后与圆点同步绘出(204~308) */
			.hr-line {
				stroke-dasharray: 400; stroke-dashoffset: 196;
				transition: stroke-dashoffset 1.2s cubic-bezier(.3,.8,.4,1);
			}
			.hr-line.draw { stroke-dashoffset: 92; }
			/* 当前点平滑滑动 */
			.hr-end-dot {
				transition: cx 1.2s cubic-bezier(.3,.8,.4,1), cy 1.2s cubic-bezier(.3,.8,.4,1);
			}
			/* 数值标签 */
			.hr-num {
				position: absolute; z-index: 5;
				font-size: 22rpx; font-weight: 700;
				padding: 2rpx 8rpx; border-radius: 10rpx;
			}
			.hr-num.a {
				bottom: 36rpx; left: 16rpx;
				background: rgba(76,175,80,0.15); color: #4CAF50;
			}
			.hr-num.b {
				top: 6rpx; left: 50%; transform: translateX(-50%);
				background: rgba(255,149,0,0.15); color: #FF9500;
			}
			.hr-num.c {
				bottom: 36rpx; right: 16rpx;
				background: rgba(255,138,61,0.15); color: #FF8A3D;
			}
			.hr-x-axis {
				position: absolute; bottom: 6rpx; left: 20rpx; right: 20rpx;
				display: flex; justify-content: space-between;
				font-size: 20rpx; color: #999; z-index: 3;
			}
			.hr-y-axis {
				position: absolute; top: 20rpx; bottom: 42rpx; left: 6rpx;
				display: flex; flex-direction: column; justify-content: space-between;
				font-size: 18rpx; color: #BBB; z-index: 3;
				text { line-height: 1; }
			}
		}

		.ac-highlight {
			font-size: 30rpx;
			font-weight: 600;
			margin-bottom: 24rpx;
			letter-spacing: 1rpx;
		}

		.text-warning {
			color: $brand-orange;
		}

		.text-danger {
			color: $color-danger;
		}

		.ac-reference {
			background: #F8F9FA;
			border-radius: 12rpx;
			padding: 16rpx 24rpx;
			font-size: 24rpx;
			color: $text-gray;
			margin-bottom: 32rpx;
		}

		.ac-actions {
			display: flex;
			gap: 24rpx;

			.btn {
				flex: 1;
				height: 80rpx;
				line-height: 80rpx;
				text-align: center;
				font-size: 30rpx;
				font-weight: 600;
				border-radius: 16rpx;
				margin: 0;
				padding: 0;
			}

			/* 橘色按钮组 */
			.btn-warning-solid {
				background: $brand-orange-grad;
				color: #FFF;
				box-shadow: 0 4rpx 12rpx rgba(255, 102, 51, 0.2);
			}

			.btn-warning-outline {
				background: #FFF;
				color: $brand-orange;
				border: 2rpx solid $brand-orange;
			}

			/* 红色按钮组 */
			.btn-danger-solid {
				background: $color-danger;
				color: #FFF;
				box-shadow: 0 4rpx 12rpx rgba(245, 63, 63, 0.2);
			}

			.btn-danger-outline {
				background: #FFF;
				color: $color-danger;
				border: 2rpx solid $color-danger;
			}
		}
	}

	/* ================== 5. 服务台账 ================== */
	.ledger-panel {
		position: relative;
		z-index: 1;
		border-radius: 32rpx;
		margin: 0 32rpx 32rpx;
		padding: 32rpx;

		background: linear-gradient(180deg, #FFEDE3 0%, #FFFFFF 100%);
		box-shadow: 0px 4rpx 16rpx 0px #F9F7F7;
		border-radius: 32rpx;
		border: 2rpx solid #FFFFFF;

		.panel-top {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 32rpx;

			.pt-left {
				text-align: center;
				display: flex;
				align-items: center;

				/* CSS 模拟文档图标 */
				.icon-book {

					margin-right: 16rpx;
				}

				.pt-title {
					margin-bottom: 10rpx;
					font-weight: 500;
					font-size: 32rpx;
					color: #2A2A2A;
				}
			}

			.btn-add {

				background: rgba(252, 118, 49, 0.2);

				color: $brand-orange;
				font-size: 26rpx;
				font-weight: 500;
				padding: 10rpx 28rpx;
				border-radius: 32rpx;
				display: flex;
				align-items: center;

				.icon-plus {
					font-size: 30rpx;
					margin-right: 6rpx;
					margin-top: -4rpx;
				}
			}
		}

		.ledger-list {
			display: flex;
			flex-direction: column;
			gap: 24rpx;
		}

		.ledger-item {
			border-radius: 32rpx;
			padding: 28rpx;
			background: #FFFFFF;
			border-radius: 16px 16px 16px 16px;
			border: 1px solid #E4E1DD;

			.li-header {
				display: flex;
				align-items: center;
				margin-bottom: 20rpx;

				.li-title {
					font-size: 30rpx;
					font-weight: 600;
					color: $text-main;
					margin-right: 16rpx;
				}

				.li-name-tag {
					font-size: 22rpx;
					color: $text-sub;
					background: #E8EAED;
					padding: 4rpx 16rpx;
					border-radius: 20rpx;
				}

				.li-status {
					margin-left: auto;
					font-size: 24rpx;
					padding: 4rpx 14rpx;
					border-radius: 8rpx;
					font-weight: 500;

					&.tag-success {
						color: $color-success;
						background: $success-light-bg;
					}

					&.tag-danger-light {
						color: $color-danger;
						background: $danger-light-bg;
					}
				}
			}

			.li-content {
				font-size: 26rpx;
				color: $text-sub;
				line-height: 1.6;
				margin-bottom: 24rpx;
				text-align: justify;
			}

			.li-footer {
				font-size: 24rpx;
				color: $text-gray;
			}

			.li-action {
				.btn-handle-small {
					display: inline-block;
					background: $brand-orange-grad;
					color: #FFF;
					font-size: 26rpx;
					font-weight: 500;
					height: 60rpx;
					line-height: 60rpx;
					padding: 0 40rpx;
					border-radius: 30rpx;
					margin: 0;
				}
			}
		}

		.expand-more {
			text-align: center;
			font-size: 26rpx;
			color: $text-gray;
			margin-top: 32rpx;
		}
	}

	/* ================== 6. 团员名单 ================== */
	.team-panel {
		position: relative;
		z-index: 1;
		border-radius: 32rpx;
		margin: 0 32rpx 40rpx;
		padding: 36rpx 32rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;


		background: linear-gradient(180deg, #FFEDE3 0%, #FFFFFF 100%);
		box-shadow: 0px 2px 4px 0px #F9F7F7;
		border-radius: 32rpx;
		border: 2rpx solid #FFFFFF;

		.tp-left {
			display: flex;
			align-items: center;

			/* 纯 CSS 双人图标示意 */
			.icon-users {

				margin-right: 16rpx;
				position: relative;
				clip-path: polygon(0 0, 100% 0, 100% 70%, 0 70%);
			}

			.tp-title {
				margin-bottom: 15rpx;
				font-size: 32rpx;
				font-weight: 600;
				color: $text-title;
			}
		}

		/* CSS下拉箭头 */
		.icon-arrow-down {
			margin-bottom: 8rpx;
		}
	}

	.safe-bottom-area {
		height: 60rpx;
	}

	/* 浪无忧吉祥物浮动动画（和首页弹窗同款） */
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

	/* ============ 导游预警弹窗 ============ */
	.warn-overlay {
		position: fixed; inset: 0; z-index: 9999;
		background: rgba(0,0,0,0.45);
		display: flex; align-items: center; justify-content: center;
		animation: fadeIn .25s ease;
	}
	@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
	.warn-modal {
		position: relative;
		width: 560rpx; background: #FFFFFF;
		border-radius: 36rpx; padding: 52rpx 40rpx 40rpx;
		text-align: center;
		box-shadow: 0 16rpx 48rpx rgba(0,0,0,0.16);
		animation: wmSlideUp .35s cubic-bezier(.22,.82,.3,1);
	}
	@keyframes wmSlideUp {
		from { transform: translateY(40rpx); opacity: 0; }
		to { transform: translateY(0); opacity: 1; }
	}
	.wm-close {
		position: absolute; top: 20rpx; right: 24rpx;
		width: 48rpx; height: 48rpx; border-radius: 50%;
		background: #F2F3F5; color: #8E8E93;
		font-size: 28rpx; display: flex; align-items: center; justify-content: center;
	}
	.wm-mascot {
		width: 160rpx; height: 160rpx;
		margin: 0 auto 16rpx;
		display: block;
		animation: mascotFloat 2.6s ease-in-out infinite;
	}
	.wm-title {
		display: block; font-size: 36rpx; font-weight: 700;
		color: #1B1E23; margin-bottom: 16rpx;
	}
	.wm-msg {
		display: block; font-size: 26rpx; color: #475467;
		line-height: 1.6; margin-bottom: 36rpx;
	}
	.wm-btn {
		width: 100%; height: 88rpx; line-height: 88rpx;
		background: linear-gradient(135deg, #FF7B52 0%, #FF5E3A 100%);
		color: #FFFFFF; font-size: 32rpx; font-weight: 600;
		border-radius: 48rpx; text-align: center;
		box-shadow: 0 8rpx 24rpx rgba(255,123,82,0.3);
	}
</style>