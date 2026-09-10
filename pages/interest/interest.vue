<template>
	<view class="page-container">
		<!-- 顶部环境渐变背景 -->
		<view class="ambient-gradient-bg"></view>

		<!-- 1. 顶部 Header (左侧导出/保存 + 右侧微信胶囊) -->
		<view class="header-section">
			<view class="action-left">
				<view class="act-btn">
					<!-- 导出图标 -->
					<image class="icon-export" src="/static/warning/daoru.png"></image>
					<text class="act-text">导出</text>
				</view>
				<view class="act-btn">
					<!-- 保存图标 -->
					<image class="icon-save" src="/static/warning/save.png"></image>
					<text class="act-text">保存</text>
				</view>
			</view>

		</view>

		<!-- 2. 兴趣识别分析顶部大卡片 -->
		<view class="analysis-card card-shadow">
			<text class="card-title-orange">{{ phase === 'analyzing' ? '兴趣识别分析中' + dots : '兴趣识别完成' }}</text>

			<!-- 进度条 -->
			<view class="progress-bar-bg">
				<view class="progress-bar-fill" :style="{ width: progress + '%' }"></view>
			</view>

			<!-- 嵌套白底“识别结果”内卡片 (带顶部 Notch 缺口) -->
		<view class="result-inner-card" v-show="phase === 'done'">
				<!-- 顶部凹槽缺口示意 -->
				<view class="notch-cutout"></view>

				<view class="result-header">
					<text class="res-title">识别结果</text>
					<view class="share-btn" @click="startExtract">
						<image class="icon-share" src="/static/warning/share.png"></image>
						<text class="share-text">分享</text>
					</view>
				</view>

				<!-- 3 个次数统计块 -->
				<view class="count-grid">
					<view class="count-box">
					<view class="num-row">
						<text class="num">{{ histNum }}</text>
						<text class="unit">次</text>
					</view>
					<text class="lbl">历史</text>
				</view>
				<view class="count-box">
					<view class="num-row">
						<text class="num">{{ fyNum }}</text>
						<text class="unit">次</text>
					</view>
					<text class="lbl">非遗</text>
				</view>
				<view class="count-box">
					<view class="num-row">
						<text class="num">{{ gkNum }}</text>
						<text class="unit">次</text>
					</view>
					<text class="lbl">港口</text>
				</view>
				</view>

				<!-- 描述文本 -->
		<!-- 		<text class="result-desc">
					通过分析 “浪无忧” 小程序里的客史档案，发现他们报名时填写的偏好关键词出奇一致。历史出现了23次，非遗出现了18次，港口一出现了15次。
				</text> -->
			</view>
		</view>

		<!-- 3. 横向 Pill 筛选 Tabs -->
		<scroll-view class="filter-scroll-row" scroll-x show-scrollbar="false">
			<view class="scroll-content">
				<view class="filter-pill active">全部 6</view>
				<view class="filter-pill">港口 2</view>
				<view class="filter-pill">历史 2</view>
				<view class="filter-pill">休闲体验 2</view>
				<view class="filter-pill">传统文化 2</view>
			</view>
		</scroll-view>

		<!-- 4. 推荐景点/行程列表 -->
		<view class="spot-list">

			<!-- 景点 1: 千年古法盐场 -->
			<view class="spot-card card-shadow">
				<image class="spot-img"
					src="/static/warning/fj1.png"
					mode="aspectFill" />
				<view class="spot-info">
					<view class="spot-top-line">
						<text class="category-tag">景点推荐</text>
						<view class="time-box">
							<view class="time-clock-icon"></view>
							<text class="time-txt">1小时</text>
						</view>
					</view>

					<text class="spot-name">花岙古法海盐晒制场</text>

					<text class="spot-desc">
						亲手上手打盐花，触摸四代传承老盐耙，沉浸式感受千百年盐农劳作日常
					</text>

					<view class="spot-tags">
						<text class="tag-orange">历史探访</text>
						<text class="tag-orange">非遗体验</text>
						<text class="tag-orange">古法盐场</text>
					</view>

					<view class="btn-row">
						<button class="btn-add-schedule">加入行程</button>
						<button class="btn-detail">详情</button>
					</view>
				</view>
			</view>

			<!-- 景点 2: 中国港口博物馆参观 -->
			<!-- <view class="spot-card card-shadow">
				<image class="spot-img"
					src="/static/warning/fj2.png"
					mode="aspectFill" />
				<view class="spot-info">
					<view class="spot-top-line">
						<text class="category-tag">景点推荐</text>
						<view class="time-box">
							<view class="time-clock-icon"></view>
							<text class="time-txt">2小时</text>
						</view>
					</view>

					<text class="spot-name">中国港口博物馆参观</text>

					<text class="spot-desc">
						国家一级博物馆，河姆渡独木舟、宋代明州港复原、现代港口实景视频；讲解通俗、分段休息，步行⩽1.5公里。
					</text>

					<view class="spot-tags">
						<text class="tag-orange">博物馆</text>
						<text class="tag-orange">历史</text>
						<text class="tag-orange">老少皆宜</text>
					</view>

					<view class="btn-row">
						<button class="btn-add-schedule">加入行程</button>
						<button class="btn-detail">详情</button>
					</view>
				</view>
			</view> -->

			<!-- 景点 3: 宁波帮博物馆 -->
			<view class="spot-card card-shadow">
				<image class="spot-img"
					src="/static/warning/fj3.png"
					mode="aspectFill" />
				<view class="spot-info">
					<view class="spot-top-line">
						<text class="category-tag">景点推荐</text>
						<view class="time-box">
							<view class="time-clock-icon"></view>
							<text class="time-txt">2小时</text>
						</view>
					</view>

					<text class="spot-name">宁波帮博物馆</text>

					<text class="spot-desc">
						不用远赴海外展馆，就在宁波帮博物馆，就能打卡独一份江海商帮人文秘境！在这里读懂游子闽海乡愁、感受两代兴学报国情怀，沉浸式感悟百年宁波帮精神。
					</text>

					<view class="spot-tags">
						<text class="tag-orange">博物馆</text>
						<text class="tag-orange">历史</text>
						<text class="tag-orange">人文探索</text>
					</view>

					<view class="btn-row">
						<button class="btn-add-schedule">加入行程</button>
						<button class="btn-detail">详情</button>
					</view>
				</view>
			</view>

		</view>

		<!-- 游客抽取分享弹窗 -->
		<view v-if="showShare" class="extract-mask" @click="maskClick">
			<view class="extract-card" @click.stop="">
				<view class="ex-header">
					<text class="ex-title">{{ selected ? '抽取完成' : '正在抽取游客' }}</text>
					<text v-if="!extracting" class="ex-close" @click="closeShare">×</text>
				</view>

				<!-- 老虎机视窗 -->
				<view class="ex-window">
					<view class="ex-row muted">
						<view class="ex-avatar" :style="{ background: prevTourist.color }">{{ prevTourist.name[0] }}</view>
						<text class="ex-name">{{ prevTourist.name }}</text>
					</view>
					<view class="ex-row highlight">
						<view class="ex-avatar" :style="{ background: curTourist.color }">{{ curTourist.name[0] }}</view>
						<text class="ex-name">{{ curTourist.name }}</text>
					</view>
					<view class="ex-row muted">
						<view class="ex-avatar" :style="{ background: nextTourist.color }">{{ nextTourist.name[0] }}</view>
						<text class="ex-name">{{ nextTourist.name }}</text>
					</view>
					<view class="ex-frame"></view>
				</view>

				<view v-if="selected" class="ex-result">
					恭喜选中 <text class="ex-pick">{{ selected.name }}</text>，将分享本次识别结果
				</view>
				<view v-else class="ex-result muted-text">抽取中…</view>

				<view class="ex-actions">
					<button v-if="selected" class="ex-btn primary">确认分享</button>
					<button class="ex-btn ghost" @click="secondaryAction">
						{{ selected ? '重新抽取' : '取消' }}
					</button>
				</view>
			</view>
		</view>

		<!-- 底部留白 -->
		<view class="safe-bottom-area"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				/* ====== 大数据分析动态效果 ====== */
				// phase: 'analyzing' 分析中 / 'done' 完成
				phase: 'analyzing',
				progress: 0,
				dots: '',
				histNum: 0,
				fyNum: 0,
				gkNum: 0,

				/* ====== 游客抽取分享 ====== */
				tourists: [
					{ name: '张奶奶', color: '#FF7043' },
					{ name: '史大爷', color: '#F53F3F' },
					{ name: '刘奶奶', color: '#00B42A' },
					{ name: '王大爷', color: '#3491FA' },
					{ name: '李爷爷', color: '#9B59B6' },
					{ name: '赵阿姨', color: '#F5A623' },
					{ name: '孙奶奶', color: '#1ABC9C' },
					{ name: '周大爷', color: '#E67E22' }
				],
				showShare: false,
				extracting: false,
				curIdx: 0,
				selected: null
			};
		},
		computed: {
			// 老虎机视窗当前高亮的游客
			curTourist() {
				return this.tourists[this.curIdx] || {};
			},
			prevTourist() {
				const len = this.tourists.length;
				return this.tourists[(this.curIdx - 1 + len) % len] || {};
			},
			nextTourist() {
				const len = this.tourists.length;
				return this.tourists[(this.curIdx + 1) % len] || {};
			}
		},
		mounted() {
			this.runAnalysis();
		},
		beforeDestroy() {
			clearInterval(this.dotTimer);
			clearInterval(this.progTimer);
			if (this.extTimer) clearTimeout(this.extTimer);
		},
		methods: {
			/* ====== 大数据分析动态效果 ====== */
			runAnalysis() {
				this.phase = 'analyzing';
				this.progress = 0;
				this.histNum = 0;
				this.fyNum = 0;
				this.gkNum = 0;
				this.dots = '';

				// 省略号动画
				let i = 0;
				this.dotTimer = setInterval(() => {
					i = (i + 1) % 4;
					this.dots = '.'.repeat(i);
				}, 400);

				// 进度条动画
				this.progTimer = setInterval(() => {
					this.progress += 2;
					if (this.progress >= 100) {
						this.progress = 100;
						clearInterval(this.progTimer);
						clearInterval(this.dotTimer);
						this.progTimer = null;
						this.dotTimer = null;
						this.dots = '';
						this.phase = 'done';
						this.countUp();
					}
				}, 60);
			},
			// 数字递增
			countUp() {
				const targets = [23, 18, 15];
				const keys = ['histNum', 'fyNum', 'gkNum'];
				const max = Math.max.apply(null, targets);
				let step = 0;
				const t = setInterval(() => {
					step++;
					keys.forEach((key, idx) => {
						this[key] = Math.min(targets[idx], Math.round(targets[idx] * step / max));
					});
					if (step >= max) {
						keys.forEach((key, idx) => { this[key] = targets[idx]; });
						clearInterval(t);
					}
				}, 40);
			},
			/* ====== 游客抽取分享 ====== */
			startExtract() {
				this.showShare = true;
				this.extracting = true;
				this.selected = null;

				const total = 26 + Math.floor(Math.random() * 10);
				const finalIdx = Math.floor(Math.random() * this.tourists.length);
				let count = 0;
				let speed = 60;

				const tick = () => {
					this.curIdx = (this.curIdx + 1) % this.tourists.length;
					count++;
					if (count > total * 0.6) speed = 110;
					if (count > total * 0.85) speed = 200;
					if (count >= total) {
						this.curIdx = finalIdx;
						this.extracting = false;
						this.selected = this.tourists[finalIdx];
						return;
					}
					this.extTimer = setTimeout(tick, speed);
				};
				tick();
			},
			reExtract() {
				if (this.extTimer) clearTimeout(this.extTimer);
				this.startExtract();
			},
			closeShare() {
				if (this.extTimer) clearTimeout(this.extTimer);
				this.extracting = false;
				this.showShare = false;
				this.selected = null;
			},
			// 弹窗遮罩点击：抽取进行中不响应
			maskClick() {
				if (!this.extracting) this.closeShare();
			},
			// 底部按钮：已选中→重新抽取，未选中→取消
			secondaryAction() {
				if (this.selected) this.reExtract();
				else this.closeShare();
			}
		}
	};
</script>

<style lang="scss" scoped>
	/* ================== 设计变量 ================== */
	$page-bg: #F7F8FA;
	$text-title: #111111;
	$text-main: #222222;
	$text-sub: #666666;
	$text-gray: #888888;

	$brand-orange: #FF5A26;
	$brand-orange-grad: linear-gradient(135deg, #FF7B47 0%, #FF4D1A 100%);
	$orange-tag-bg: #FFF2EC;
	$orange-card-bg: linear-gradient(180deg, #FFEBDD 0%, #FFFDFB 40%, #FFFFFF 100%);

	/* ================== 全局重置 ================== */
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

	.card-shadow {
		box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.03);
	}

	/* 顶部光晕背景 */
	.ambient-gradient-bg {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 550rpx;
		background-image: url(/static/bg.png);
		background-size: 100% 100%;
		z-index: 0;
	}

	/* ================== 1. 顶部 Header ================== */
	.header-section {
		position: relative;
		z-index: 1;
		padding: 100rpx 32rpx 24rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;

		.action-left {
			display: flex;
			gap: 28rpx;
			align-items: center;

			.act-btn {
				display: flex;
				align-items: center;
				gap: 8rpx;

				.act-text {
					font-size: 28rpx;
					font-weight: 500;
					color: #222;
				}

				/* CSS 纯代码绘制精致图标 */
				.icon-export {
					width: 22rpx;
					height: 22rpx;
					// border: 3rpx solid #222;
					border-top: none;
					position: relative;
					margin-top: 6rpx;

					&::after {
						content: '';
						position: absolute;
						top: -12rpx;
						left: 5rpx;
						width: 0;
						height: 0;
						border-left: 6rpx solid transparent;
						border-right: 6rpx solid transparent;
						border-bottom: 10rpx solid #222;
					}
				}

				.icon-save {
					width: 24rpx;
					height: 24rpx;
					// border: 3rpx solid #222;
					// border-radius: 4rpx;
					position: relative;

					&::after {
						content: '';
						position: absolute;
						top: 2rpx;
						left: 5rpx;
						width: 10rpx;
						height: 8rpx;
						background: #222;
					}
				}
			}
		}

		/* 微信胶囊 1:1 还原 */
		.wechat-capsule {
			display: flex;
			align-items: center;
			justify-content: center;
			width: 174rpx;
			height: 64rpx;
			background: rgba(255, 255, 255, 0.65);
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

	/* ================== 2. 兴趣识别大卡片 ================== */
	.analysis-card {
		position: relative;
		z-index: 1;
		margin: 10rpx 32rpx 32rpx;
		// padding: 36rpx 0rpx 0rpx;
		background: rgba(255, 255, 255, 0.5);

		border: 4rpx solid #FFFFFF;

		border-radius: 36rpx;

		.card-title-orange {
			font-size: 36rpx;
			font-weight: bold;
			display: block;
			margin-bottom: 20rpx;
			letter-spacing: 1rpx;
			margin-top: 32rpx;
			margin-left: 48rpx;

			color: #FC7631;
		}

		/* 进度条 */
		.progress-bar-bg {
			// width: 100%;
			height: 12rpx;
			background: rgba(255, 90, 38, 0.15);
			border-radius: 6rpx;
			margin-top: 46rpx;
			margin-left: 48rpx;
			margin-right: 48rpx;
			margin-bottom: 69rpx;
			overflow: hidden;

			.progress-bar-fill {
				width: 42%;
				height: 100%;
				background: $brand-orange-grad;
				border-radius: 6rpx;
			}
		}

		/* 嵌套白底“识别结果”内卡片 */
		.result-inner-card {
			position: relative;
			background: #FFF3E9;
			background-image: url(/static/warning/rege.png);

			// border: 6rpx solid #FFFFFF;
			background-size: 100% 100%;
			border-radius: 28rpx;
			padding: 32rpx 28rpx 28rpx;
			// box-shadow: 0 6rpx 20rpx rgba(255, 90, 38, 0.05);

			/* 顶部向下弧形凹槽缺口 (Notch) */
			// .notch-cutout {
			// 	position: absolute;
			// 	top: 0;
			// 	left: 50%;
			// 	transform: translateX(-50%);
			// 	width: 120rpx;
			// 	height: 50rpx;
			// 	background: #FFF;
			// 	/* 与外层橘色背景完美衔接 */
			// 	border-bottom-left-radius: 50rpx;
			// 	border-bottom-right-radius: 50rpx;
			// }

			.result-header {
				display: flex;
				justify-content: space-between;
				align-items: center;
				margin-bottom: 24rpx;

				.res-title {
					font-size: 32rpx;
					font-weight: bold;
					color: $brand-orange;
				}

				.share-btn {
					display: flex;
					align-items: center;
					gap: 8rpx;
					font-size: 24rpx;
					color: $text-sub;

					.icon-share {
						width: 24rpx;
						height: 24rpx;
					}
				}
			}

			/* 3 个次数统计块 */
			.count-grid {
				display: flex;
				justify-content: space-between;
				gap: 16rpx;
				margin-bottom: 24rpx;

				.count-box {
					// flex: 1;
					width: 180rpx;
					height: 176rpx;
					background: rgba(255,255,255,0.5);
					border-radius: 48rpx;
					border: 1px solid #FFFFFF;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;


					background: rgba(255, 255, 255, 0.5);
					border-radius: 48rpx;
					border: 2rpx solid #FFFFFF;

					.num-row {
						display: flex;
						align-items: baseline;
						margin-bottom: 6rpx;

						.num {
							font-size: 44rpx;
							font-weight: bold;
							color: #2A2A2A;
							line-height: 1;
						}

						.unit {
							font-size: 22rpx;
							color: #2A2A2A;
							margin-left: 4rpx;
							font-weight: bold;
						}
					}

					.lbl {
						font-size: 22rpx;
						color: #2A2A2A;
					}
				}
			}

			.result-desc {
				font-size: 25rpx;
				color: $text-sub;
				line-height: 1.6;
				text-align: justify;
				display: block;
			}
		}
	}

	/* ================== 3. 横向 Tab 筛选 ================== */
	.filter-scroll-row {
		position: relative;
		z-index: 1;
		white-space: nowrap;
		margin-bottom: 32rpx;
		width: 100%;

		.scroll-content {
			display: inline-flex;
			gap: 16rpx;
			padding: 0 32rpx;

			.filter-pill {
				display: inline-block;
				padding: 14rpx 36rpx;
				font-size: 26rpx;
				font-weight: 500;
				border-radius: 40rpx;
				background: #FFFFFF;
				color: $text-main;
				border: 1rpx solid #E5E6EB;

				&.active {
					background: $brand-orange-grad;
					color: #FFFFFF;
					border: none;
					box-shadow: 0 4rpx 14rpx rgba(255, 90, 38, 0.3);
				}
			}
		}
	}

	/* ================== 4. 景点列表 ================== */
	.spot-list {
		position: relative;
		z-index: 1;
		margin: 0 32rpx;
		display: flex;
		flex-direction: column;
		gap: 32rpx;
	}

	.spot-card {
		background: #FFFFFF;
		border-radius: 32rpx;
		padding: 28rpx;
		display: flex;
		gap: 24rpx;

		.spot-img {
			width: 200rpx;
			height: 200rpx;
			border-radius: 20rpx;
			flex-shrink: 0;
			background: #F0F0F0;
		}

		.spot-info {
			flex: 1;
			display: flex;
			flex-direction: column;

			.spot-top-line {
				display: flex;
				justify-content: space-between;
				align-items: center;
				margin-bottom: 10rpx;

				.category-tag {
					font-size: 20rpx;
					color: $text-sub;
					border: 1rpx solid #D2D5DA;
					padding: 2rpx 12rpx;
					border-radius: 20rpx;
				}

				.time-box {
					display: flex;
					align-items: center;
					gap: 6rpx;
					font-size: 22rpx;
					color: $text-sub;

					.time-clock-icon {
						width: 20rpx;
						height: 20rpx;
						border: 2rpx solid $text-sub;
						border-radius: 50%;
						position: relative;

						&::after {
							content: '';
							position: absolute;
							top: 3rpx;
							left: 8rpx;
							width: 2rpx;
							height: 6rpx;
							background: $text-sub;
						}
					}
				}
			}

			.spot-name {
				font-size: 32rpx;
				font-weight: bold;
				color: $text-title;
				margin-bottom: 10rpx;
				line-height: 1.2;
			}

			.spot-desc {
				font-size: 24rpx;
				color: $text-sub;
				line-height: 1.5;
				margin-bottom: 16rpx;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				overflow: hidden;
				text-overflow: ellipsis;
			}

			.spot-tags {
				display: flex;
				flex-wrap: wrap;
				gap: 12rpx;
				margin-bottom: 24rpx;

				.tag-orange {
					font-size: 20rpx;
					color: $brand-orange;
					background: $orange-tag-bg;
					padding: 4rpx 14rpx;
					border-radius: 8rpx;
					font-weight: 500;
				}
			}

			.btn-row {
				display: flex;
				gap: 16rpx;

				button {
					height: 64rpx;
					line-height: 64rpx;
					font-size: 26rpx;
					font-weight: bold;
					border-radius: 32rpx;
					margin: 0;
					padding: 0 32rpx;
				}

				.btn-add-schedule {
					background: $brand-orange-grad;
					color: #FFFFFF;
					box-shadow: 0 4rpx 12rpx rgba(255, 90, 38, 0.25);
				}

				.btn-detail {
					background: #F2F3F5;
					color: $text-sub;
				}
			}
		}
	}

	.safe-bottom-area {
		height: 60rpx;
	}

	/* ====== 分析动态效果补充样式 ====== */
	.progress-bar-fill {
		transition: width 0.12s linear;
	}

	.result-inner-card {
		animation: exFadeInUp 0.5s ease both;
	}

	@keyframes exFadeInUp {
		from {
			opacity: 0;
			transform: translateY(20rpx);
		}

		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* ====== 游客抽取分享弹窗 ====== */
	.extract-mask {
		position: fixed;
		left: 0;
		top: 0;
		right: 0;
		bottom: 0;
		background: rgba(0, 0, 0, 0.55);
		z-index: 999;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.extract-card {
		width: 560rpx;
		background: #FFFFFF;
		border-radius: 32rpx;
		padding: 40rpx 32rpx 32rpx;
		box-shadow: 0 20rpx 50rpx rgba(0, 0, 0, 0.2);

		.ex-header {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 32rpx;

			.ex-title {
				font-size: 34rpx;
				font-weight: bold;
				color: #222;
			}

			.ex-close {
				font-size: 44rpx;
				color: #999;
				line-height: 1;
			}
		}

		.ex-window {
			position: relative;
			height: 360rpx;
			border-radius: 24rpx;
			background: #F5F6F8;
			overflow: hidden;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;

			.ex-row {
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: center;
				gap: 20rpx;
				height: 120rpx;
				opacity: 0.35;

				&.highlight {
					opacity: 1;
					transform: scale(1.06);
				}

				.ex-avatar {
					width: 80rpx;
					height: 80rpx;
					border-radius: 50%;
					color: #FFF;
					font-size: 32rpx;
					font-weight: bold;
					display: flex;
					align-items: center;
					justify-content: center;
				}

				.ex-name {
					font-size: 34rpx;
					font-weight: 600;
					color: #222;
				}
			}

			.ex-frame {
				position: absolute;
				top: 50%;
				left: 24rpx;
				right: 24rpx;
				height: 120rpx;
				transform: translateY(-50%);
				border: 2rpx solid #FF5A26;
				border-radius: 20rpx;
				box-shadow: 0 0 0 6rpx rgba(255, 90, 38, 0.12);
				pointer-events: none;
			}
		}

		.ex-result {
			margin-top: 32rpx;
			text-align: center;
			font-size: 28rpx;
			color: #333;

			.ex-pick {
				color: #FF5A26;
				font-weight: bold;
				margin: 0 6rpx;
			}

			&.muted-text {
				color: #999;
			}
		}

		.ex-actions {
			display: flex;
			gap: 20rpx;
			margin-top: 36rpx;

			.ex-btn {
				flex: 1;
				height: 80rpx;
				line-height: 80rpx;
				font-size: 28rpx;
				font-weight: 600;
				border-radius: 40rpx;
				margin: 0;
				padding: 0;

				&.primary {
					background: linear-gradient(135deg, #FF7B47 0%, #FF4D1A 100%);
					color: #FFF;
					box-shadow: 0 6rpx 16rpx rgba(255, 90, 38, 0.3);
				}

				&.ghost {
					background: #F2F3F5;
					color: #666;
				}
			}
		}
	}
</style>