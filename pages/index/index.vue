<template>
	<view class="page-container">
		<!-- 顶部环境渐变背景 -->
		<view class="ambient-bg"></view>

		<!-- 顶部 Header -->
		<view class="header">
			<view class="title-box">
				<text class="title-main">浪无忧</text>
				<text class="title-sub">银龄定制游，出行更安心</text>
			</view>
		</view>

		<!-- 核心数据 Banner (橘色渐变) -->
		<view class="banner">
			<view class="day-tag">第2天</view>

			<view>
				<text class="banner-title">向海而生，情暖银龄</text>
				<text class="banner-sub">中国海洋文化二日游</text>

				<view class="banner-stats">
					<view class="stat-item">
						<text class="num">30</text>
						<text class="label">团队总数(人)</text>
					</view>
					<view class="stat-item">
						<text class="num">30</text>
						<text class="label">集合人数</text>
					</view>
					<view class="stat-item">
						<text class="num">2</text>
						<text class="label">行程天数</text>
					</view>
				</view>
			</view>

		</view>

		<!-- 1. 团体健康状况 -->
		<view class="section">
			<view class="section-head">
				<view class="left-title">
					<view class="icon-circle"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"
							xmlns="http://www.w3.org/2000/svg">
							<path
								d="M1.85148 7.73133C1.78985 7.60103 1.73257 7.46893 1.68028 7.3352C1.46413 6.78243 1.33325 6.2014 1.33325 5.6C1.33325 3.61177 2.96131 2 4.96962 2C6.23445 2 7.34845 2.63931 7.99992 3.60933C8.65138 2.63931 9.76538 2 11.0302 2C13.0385 2 14.6666 3.61177 14.6666 5.6C14.6666 8.18823 12.2424 10.4 11.0302 11.6C10.2222 12.4 9.21205 13.2 7.99992 14C6.78778 13.2 5.77768 12.4 4.96962 11.6C4.84758 11.4792 4.71329 11.3481 4.57039 11.2075"
								stroke="#2A2A2A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
							<path d="M2.66675 9.99112L6.37135 6.34652L8.52611 8.56862L11.754 5.27292" stroke="#FC7631"
								stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
						</svg>
					</view>
					<text class="txt">团体健康状况</text>
				</view>
				<view class="btn-refresh">实时更新</view>
			</view>

			<view class="card">
				<view class="unit-text">单位：人</view>

				<view class="chart-row">
					<!-- 纯 CSS 环形进度条 -->
					<view class="donut-chart">
						<view class="donut-inner">
							<text class="val">96.7%</text>
							<text class="lbl">健康率</text>
						</view>
					</view>

					<view class="legend-box">
						<view class="legend-item">
							<view class="dot green"></view><text class="name">正常</text><text class="count">29</text>
						</view>
						<view class="legend-item">
							<view class="dot orange"></view><text class="name">预警中</text><text class="count">1</text>
						</view>
						<view class="legend-item">
							<view class="dot red"></view><text class="name">危急</text><text class="count">0</text>
						</view>
					</view>
				</view>

				<view class="person-list">
					<!-- 张爷爷 (预警：血糖偏低) -->
					<view class="person-card orange-style">
						<view class="p-head">
							<view class="p-info">
								<view style="display: flex;align-items: center;">
									<view class="dot-small orange"></view>
									<text class="p-name">张爷爷</text>
									<text class="p-tag orange-tag">预警</text>
								</view>
							</view>
						</view>
						<view class="p-desc-row">
							<view class="p-desc">血糖偏低，已提醒减少活动</view>
							<image src="/static/index/down.png" style="width: 26rpx;height: 26rpx;"></image>
						</view>

						<view class="p-divider"></view>

						<!-- 血糖值波动曲线：从正常降到偏低 -->
						<view class="sugar-chart-wrap">
							<view class="sugar-title">
								<text class="st">血糖波动（mmol/L）</text>
								<view class="st-legend">
									<view class="leg-dot normal"></view><text>正常区</text>
									<view class="leg-dot low" style="margin-left: 16rpx;"></view><text>偏低区</text>
								</view>
							</view>
							<view class="sugar-chart">
								<view class="range-normal"></view>
								<view class="range-low"></view>
								<view class="ref-line ref-low"><text class="ref-txt">3.9</text></view>
								<view class="ref-line ref-hi"><text class="ref-txt">6.1</text></view>
								<svg class="sugar-svg" viewBox="0 0 560 180" preserveAspectRatio="none">
									<defs>
										<linearGradient id="sugarFill" x1="0" y1="0" x2="0" y2="1">
											<stop offset="0%" stop-color="#FC7631" stop-opacity="0.28" />
											<stop offset="100%" stop-color="#FC7631" stop-opacity="0" />
										</linearGradient>
										<linearGradient id="sugarLine" x1="0" y1="0" x2="1" y2="0">
											<stop offset="0%" stop-color="#00B42A" />
											<stop offset="48%" stop-color="#F53F3F" />
											<stop offset="100%" stop-color="#00B42A" />
										</linearGradient>
									</defs>
									<polyline
										class="sugar-line"
										:class="{ draw: chartAnim }"
										points="0,55 100,62 180,82 240,115 280,155 340,130 410,108 490,95 560,88"
										fill="none"
										stroke="url(#sugarLine)"
										stroke-width="4"
										stroke-linecap="round"
										stroke-linejoin="round" />
									<polygon
										class="sugar-area"
										:class="{ draw: chartAnim }"
										points="0,55 100,62 180,82 240,115 280,155 340,130 410,108 490,95 560,88 560,180 0,180"
										fill="url(#sugarFill)" />
									<!-- 起点 正常 5.2 -->
									<circle cx="0" cy="55" r="6" fill="#00B42A" />
									<circle cx="0" cy="55" r="11" fill="#00B42A" fill-opacity="0.2" />
									<!-- 低点 预警 3.6 高亮 -->
									<circle cx="280" cy="155" r="8" fill="#F53F3F" />
									<circle cx="280" cy="155" r="14" fill="#F53F3F" fill-opacity="0.2" />
									<!-- 终点 恢复 4.8 -->
									<circle cx="560" cy="88" r="6" fill="#00B42A" />
									<circle cx="560" cy="88" r="11" fill="#00B42A" fill-opacity="0.2" />
								</svg>
								<view class="x-axis">
									<text>10:00</text>
									<text>10:30</text>
									<text>11:00</text>
								</view>
								<view class="val-label start">5.2 正常</view>
								<view class="val-label mid">3.6 预警</view>
								<view class="val-label end">4.8 恢复</view>
							</view>

							<!-- 体征前后对比 -->
							<view class="cmp-row">
								<view class="cmp-col before">
									<view class="cmp-tag">
										<view class="c-dot red"></view>
										<text>处理前</text>
									</view>
									<view class="cmp-items">
										<view class="ci-item">
											<text class="ci-num">3.6</text>
											<text class="ci-unit">mmol/L</text>
											<text class="ci-label">血糖</text>
										</view>
										<view class="ci-row">
											<view class="ci-sm">
												<text class="cs-num">76</text>
												<text class="cs-label">心率</text>
											</view>
											<view class="ci-sm">
												<text class="cs-num">120/78</text>
												<text class="cs-label">血压</text>
											</view>
										</view>
										<view class="ci-row">
											<view class="ci-sm">
												<text class="cs-num">96%</text>
												<text class="cs-label">血氧</text>
											</view>
											<view class="ci-sm">
												<text class="cs-num">36.5°</text>
												<text class="cs-label">体温</text>
											</view>
										</view>
									</view>
								</view>
								<view class="cmp-arrow">
									<view class="ca-gel">补糖凝胶</view>
									<text>→</text>
								</view>
								<view class="cmp-col after">
									<view class="cmp-tag">
										<view class="c-dot green"></view>
										<text>处理后</text>
									</view>
									<view class="cmp-items">
										<view class="ci-item">
											<text class="ci-num ok">4.8</text>
											<text class="ci-unit">mmol/L</text>
											<text class="ci-label">血糖</text>
										</view>
										<view class="ci-row">
											<view class="ci-sm">
												<text class="cs-num">72</text>
												<text class="cs-label">心率</text>
											</view>
											<view class="ci-sm">
												<text class="cs-num">122/78</text>
												<text class="cs-label">血压</text>
											</view>
										</view>
										<view class="ci-row">
											<view class="ci-sm">
												<text class="cs-num">96%</text>
												<text class="cs-label">血氧</text>
											</view>
											<view class="ci-sm">
												<text class="cs-num">36.5°</text>
												<text class="cs-label">体温</text>
											</view>
										</view>
									</view>
								</view>
							</view>

							<view class="goto-sugar" @click="goSugar">
								<text>查看血糖恢复方案</text>
								<text class="arrow">›</text>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>

		<!-- 2. 应急处理 -->
		<view class="section">
			<view class="section-head">
				<view class="left-title">
					<view class="icon-circle"><svg width="16" height="16" viewBox="0 0 16 16" fill="none"
							xmlns="http://www.w3.org/2000/svg">
							<path
								d="M1.85148 7.73133C1.78985 7.60103 1.73257 7.46893 1.68028 7.3352C1.46413 6.78243 1.33325 6.2014 1.33325 5.6C1.33325 3.61177 2.96131 2 4.96962 2C6.23445 2 7.34845 2.63931 7.99992 3.60933C8.65138 2.63931 9.76538 2 11.0302 2C13.0385 2 14.6666 3.61177 14.6666 5.6C14.6666 8.18823 12.2424 10.4 11.0302 11.6C10.2222 12.4 9.21205 13.2 7.99992 14C6.78778 13.2 5.77768 12.4 4.96962 11.6C4.84758 11.4792 4.71329 11.3481 4.57039 11.2075"
								stroke="#2A2A2A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
							<path d="M2.66675 9.99112L6.37135 6.34652L8.52611 8.56862L11.754 5.27292" stroke="#FC7631"
								stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
						</svg></view>
					<text class="txt">应急处理</text>
				</view>
			</view>

			<view class="card padding-0">
				<view class="filter-wrap">
					<view class="filter-pill">1项未处理</view>
				</view>

				<view class="divider-line"></view>

				<view class="emergency-item">
					<view class="e-top">
						<text class="tag-outline orange">预警</text>
						<text class="e-title">张爷爷 血糖偏低</text>
						<text class="e-status red">待处理</text>
					</view>
					<view class="e-desc">实时监测血糖 3.6 mmol/L（偏低），已提醒减少活动，注意补充糖分</view>
					<view class="e-action">
						<view class="btn-outline-orange">立即处理</view>
					</view>
				</view>

				<view class="divider-line"></view>

				<view class="emergency-item">
					<view class="e-top">
						<text class="tag-outline orange">预警</text>
						<text class="e-title">张爷爷 血糖偏高</text>
						<text class="e-status gray">已处理</text>
					</view>
					<view class="e-desc">血糖波动记录，已提醒服药休息，减少走动活动</view>
					<view class="e-footer">处理人: 海安</view>
				</view>
			</view>
		</view>

		<!-- ================= 1. 今日行程 模块 ================= -->
		<view class="schedule-section">
			<!-- 模块头部 -->
			<view class="schedule-header">
				<view class="sh-left">
					<view class="icon-orange-sq">
						<text class="sq-txt">30</text>
					</view>
					<text class="sh-title">今日行程</text>
					<text class="sh-sub">7月4日 完成1/5</text>
				</view>
				<view class="sh-arrow-btn">
					<view class="arrow-up"></view>
				</view>
			</view>

			<!-- 双盒排版行程列表 -->
			<view class="itinerary-wrapper">

				<!-- 节点 1：进行中/选中（黑橙暗色高亮） -->
				<view class="itinerary-row active-row">
					<view class="icon-box active-box">
						<!-- 景点图标 -->
						<image class="custom-icon" src="/static/index/icon-orange1.png"></image>
					</view>
					<view class="card-box active-card">
						<view class="card-top">
							<text class="title orange-txt">前往象山花岙岛</text>
							<text class="time orange-sub-txt">8:30-10:10</text>
						</view>
						<view class="card-bottom">
							<image class="loc-pin" src="/static/index/map.png"></image>
							<text class="loc-name">象山</text>
						</view>
					</view>
				</view>

				<!-- 节点 2：普通景点（纯白卡片） -->
				<view class="itinerary-row">
					<view class="icon-box">
						<image class="custom-icon" src="/static/index/icon-orange2.png"></image>
					</view>
					<view class="card-box">
						<view class="card-top">
							<text class="title">花岙岛古法盐田非遗体验...</text>
							<text class="time">10:10-11:30</text>
						</view>
						<view class="card-bottom">
							<image class="loc-pin" src="/static/index/map.png"></image>
							<text class="loc-name">花岙岛</text>
						</view>
					</view>
				</view>

				<!-- 节点 3：午餐（纯白卡片） -->
				<view class="itinerary-row">
					<view class="icon-box">
						<image class="custom-icon" src="/static/index/icon-orange3.png"></image>
					</view>
					<view class="card-box">
						<view class="card-top">
							<text class="title">午餐</text>
							<text class="time">11:30-13:40</text>
						</view>
						<view class="card-bottom">
							<image class="loc-pin" src="/static/index/map.png"></image>
							<text class="loc-name">象山农家盐田宴</text>
						</view>
					</view>
				</view>

				<!-- 节点 4：普通景点（纯白卡片） -->
				<view class="itinerary-row">
					<view class="icon-box">
						<image class="custom-icon" src="/static/index/icon-orange2.png"></image>
					</view>
					<view class="card-box">
						<view class="card-top">
							<text class="title">前往中国港口博物馆</text>
							<text class="time">13:40-14:50</text>
						</view>
						<view class="card-bottom">
							<image class="loc-pin" src="/static/index/map.png"></image>
							<text class="loc-name">中国港口博物馆</text>
						</view>
					</view>
				</view>
				<view class="itinerary-row">
					<view class="icon-box">
						<image class="custom-icon" src="/static/index/icon-orange2.png"></image>
					</view>
					<view class="card-box">
						<view class="card-top">
							<text class="title">中国港口博物馆参观</text>
							<text class="time">15:00-17:00</text>
						</view>
						<view class="card-bottom">
							<image class="loc-pin" src="/static/index/map.png"></image>
							<text class="loc-name">中国港口博物馆</text>
						</view>
					</view>
				</view>

				<!-- 节点 5：底部渐隐节点 -->
				<view class="itinerary-row fade-row">
					<view class="icon-box">
						<image class="custom-icon" src="/static/index/icon-orange4.png"></image>
					</view>
					<view class="card-box">
						<view class="card-top">
							<text class="title">统一接机/接站</text>
							<text class="time">15:00-17:00</text>
						</view>
						<view class="card-bottom">
							<image class="loc-pin" src="/static/index/map.png"></image>
							<text class="loc-name">机场/车站</text>
						</view>
					</view>
				</view>

				<!-- 展开蒙层 + Pill 按钮 -->
				<view class="expand-overlay">
					<view class="expand-pill-btn">
						<text class="btn-txt">展开查看全部</text>
						<view class="arrow-down-orange"></view>
					</view>
				</view>
			</view>
		</view>


		<!-- ================= 2. 服务台账 模块 ================= -->
		<view class="ledger-card-section">
			<!-- 模块头部（带粉橙色背景渐变） -->
			<view class="ledger-header">
				<view class="lh-left">
					<view class="icon-book-mark"></view>
					<text class="lh-title">服务台账</text>
				</view>
				<view class="lh-add-btn">
					<text class="plus-symbol">⊕</text>
					<text class="add-txt">新增</text>
				</view>
			</view>

			<!-- 记录卡片列表 -->
			<view class="record-list">

				<!-- 记录 1：已处理 -->
				<view class="record-item">
					<view class="ri-top">
						<text class="ri-title">血压异常处置记录</text>
						<text class="user-pill-tag">刘奶奶</text>
						<text class="status-pill-tag tag-green">已处理</text>
					</view>
					<text class="ri-desc">
						09:15血压152/96，血氧95%，安排游客坐下休息，联系随行医护，暂时退出参观活动，等待进一步评估。
					</text>
					<view class="ri-footer">
						处理人：海安
					</view>
				</view>

				<!-- 记录 2：待处理 (带按钮) -->
				<view class="record-item">
					<view class="ri-top">
						<text class="ri-title">血压异常处置记录</text>
						<text class="user-pill-tag">刘奶奶</text>
						<text class="status-pill-tag tag-red">待处理</text>
					</view>
					<text class="ri-desc">
						09:15血压152/96，血氧95%，安排游客坐下休息，联系随行医护，暂时退出参观活动，等待进一步评估。
					</text>
					<view class="ri-action">
						<button class="btn-handle-orange">立即处理</button>
					</view>
				</view>

				<!-- 记录 3：已处理 -->
				<view class="record-item">
					<view class="ri-top">
						<text class="ri-title">血压异常处置记录</text>
						<text class="user-pill-tag">刘奶奶</text>
						<text class="status-pill-tag tag-green">已处理</text>
					</view>
					<text class="ri-desc">
						09:15血压152/96，血氧95%，安排游客坐下休息，联系随行医护，暂时退出参观活动，等待进一步评估。
					</text>
					<view class="ri-footer">
						处理人：海安
					</view>
				</view>

			</view>
		</view>

		<!-- 引入并使用弹窗组件 -->
		<RiskWarningModal :visible.sync="showWarning" targetName="张爷爷" @check="goToDetail" />


		<!-- 底部安全区留白 -->
		<view class="safe-bottom"></view>
	</view>
</template>

<script>
	import RiskWarningModal from '@/components/RiskWarningModal/RiskWarningModal.vue'

	export default {
		components: {
			RiskWarningModal
		},
		data() {
			return {
				showWarning: true, // 默认显示用于测试
				chartAnim: false // 血糖波动折线动画开关
			}
		},
		mounted() {
			// 页面加载后触发血糖折线绘制动画
			this.animTimer = setTimeout(() => {
				this.chartAnim = true;
			}, 300);
		},
		beforeDestroy() {
			if (this.animTimer) clearTimeout(this.animTimer);
		},
		methods: {
			goToDetail() {
				uni.showToast({
					title: '正在前往查看...',
					icon: 'none'
				})
				// uni.navigateTo({ url: '...' })
			},
			goSugar() {
				uni.navigateTo({ url: '/pages/sugar/sugar' });
			}
		}
	}
</script>

<style lang="scss" scoped>
	/* 全局色彩与变量 */
	$bg-main: #F8F7F4;
	$brand-orange: #FF7B52;
	$brand-orange-light: #FFF2E8;
	$text-main: #222222;
	$text-sub: #888888;
	$color-green: #00C05A;
	$color-red: #FF4D4F;
	$color-orange: #FA8C16;

	.page-container {
		min-height: 100vh;
		padding-bottom: 50rpx;
		background-color: $bg-main;
		position: relative;
		font-family: "PingFang SC", -apple-system, sans-serif;
		overflow-x: hidden;
	}

	/* 顶部环境渐变 */
	.ambient-bg {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 500rpx;
		background-image: url(/static/bg.png);
		background-size: 100% 100%;
		z-index: 0;
	}

	/* 头部 */
	.header {
		position: relative;
		z-index: 1;
		padding: 80rpx 40rpx 30rpx;
		display: flex;
		justify-content: space-between;
		align-items: flex-end;

		.title-box {
			display: flex;
			flex-direction: column;

			.title-main {
				font-size: 48rpx;
				font-weight: bold;
				color: #111;
				line-height: 1.2;
			}

			.title-sub {
				font-size: 28rpx;
				font-weight: bold;
				color: #111;
				line-height: 1.2;
				margin-top: 10rpx;
			}
		}

		.action-capsule {
			display: flex;
			align-items: center;
			background: rgba(255, 255, 255, 0.7);
			border: 2rpx solid rgba(255, 255, 255, 0.9);
			border-radius: 40rpx;
			padding: 10rpx 24rpx;
			backdrop-filter: blur(10px);

			.icon-btn {
				font-size: 32rpx;
				color: #333;
			}

			.divider {
				width: 2rpx;
				height: 24rpx;
				background: #CCC;
				margin: 0 16rpx;
			}
		}
	}

	/* 横幅 Banner */
	.banner {
		position: relative;
		z-index: 1;
		margin: 10rpx 30rpx 40rpx;
		background-image: url(/static/index/range.png);
		background-size: 100% 100%;
		// background-repeat: no-repeat;

		border-radius: 32rpx;
		padding: 40rpx 40rpx 30rpx;
		color: #FFF;

		// box-shadow: 0 16rpx 32rpx rgba(255, 123, 82, 0.25);

		.svg-layout {
			position: absolute;
			top: 0rpx;
			left: 0rpx;
			z-index: -1;
			width: 100%;
		}


		.day-tag {
			position: absolute;
			top: 0;
			right: 25rpx;
			background-color: #FFF;
			color: $brand-orange;
			font-size: 22rpx;
			font-weight: bold;
			width: 65px;
			height: 22px;
			border-radius: 20rpx;
			display: flex;
			align-items: center;
			justify-content: center;
		}

		.banner-title {
			display: block;
			font-size: 48rpx;
			font-weight: 700;
			margin-bottom: 1rpx;
			letter-spacing: 1px;
		}

		.banner-sub {
			display: block;
			font-size: 48rpx;
			font-weight: 700;
			letter-spacing: 1px;
		}

		.banner-stats {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-top: 30rpx;
			// margin-bottom: 50rpx;

			.stat-item {
				display: flex;
				flex-direction: column;


				.num {
					font-size: 64rpx;
					font-weight: bold;
					line-height: 1;
				}

				.label {
					font-size: 28rpx;
					opacity: 0.8;
					margin-top: 12rpx;
				}
			}
		}
	}

	/* 模块通用样式 */
	.section {
		position: relative;
		z-index: 1;
		margin-bottom: 40rpx;

		.section-head {
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 0 40rpx;
			margin-bottom: 24rpx;

			.left-title {
				display: flex;
				align-items: center;

				.icon-circle {
					width: 36rpx;
					height: 36rpx;
					border-radius: 50%;
					// border: 2rpx solid #666;
					display: flex;
					align-items: center;
					justify-content: center;
					margin-right: 12rpx;

					.icon {
						font-size: 20rpx;
						color: #666;
					}
				}

				.txt {
					font-size: 32rpx;
					font-weight: 600;
					color: $text-main;
				}
			}

			.btn-refresh,
			.btn-detail {
				background: $brand-orange-light;
				color: $brand-orange;
				font-size: 22rpx;
				padding: 6rpx 20rpx;
				border-radius: 20rpx;
				font-weight: 500;
			}

			.right-text {
				font-size: 24rpx;
				color: $text-sub;
			}
		}
	}

	/* 通用白底卡片 */
	.card {

		font-weight: 400;
		font-size: 28rpx;
		color: #595959;

		background: #FFFFFF;
		border-radius: 32rpx;
		margin: 0 32rpx;
		padding: 30rpx;
		box-shadow: 0 4rpx 16rpx rgba(0, 0, 0, 0.03);

		&.padding-0 {
			padding: 0;

			background: linear-gradient(180deg, #FFEDE3 0%, #FFFFFF 100%);
		}
	}

	/* --- 1. 健康状况卡片 --- */
	.unit-text {
		font-size: 22rpx;
		color: $text-sub;
		margin-bottom: 20rpx;
	}

	.chart-row {
		display: flex;
		align-items: center;
		margin-bottom: 40rpx;

		.donut-chart {
			width: 226rpx;
			height: 226rpx;
			border-radius: 50%;
			/* 纯 CSS 环形，96.7%绿色，其余橘色（1位预警） */
			background: conic-gradient($color-green 0% 96.7%, #FC7631 96.7% 100%);
			display: flex;
			align-items: center;
			justify-content: center;
			margin-right: 50rpx;
			margin-left: 20rpx;

			.donut-inner {
				width: 182rpx;
				height: 182rpx;
				border-radius: 50%;
				background: #FFFFFF;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;

				.val {
					font-size: 36rpx;
					font-weight: bold;
					color: $text-main;
					line-height: 1.1;
				}

				.lbl {
					font-size: 18rpx;
					color: $text-sub;
				}
			}
		}

		.legend-box {
			flex: 1;
			margin-left: 58rpx;


			.legend-item {
				display: flex;
				align-items: center;
				margin-bottom: 32rpx;
				font-family: Source Han Sans CN, Source Han Sans CN;
				font-weight: 400;
				font-size: 32rpx;
				color: #2A2A2A;

				&:last-child {
					margin-bottom: 0;
				}

				.dot {
					width: 20rpx;
					height: 20rpx;
					border-radius: 50%;
					margin-right: 16rpx;
				}

				.green {
					background: $color-green;
				}

				.orange {
					background: $color-orange;
				}

				.red {
					background: $color-red;
				}

				.name {
					width: 100rpx;
				}

				.count {
					font-weight: bold;
					margin-left: auto;
					padding-right: 20rpx;
				}
			}
		}
	}

	/* 人员微卡片 */
	.person-card {
		border-radius: 16rpx;
		padding: 24rpx;
		margin-bottom: 20rpx;
		background: #FFFFFF;
		border: 2rpx solid transparent;




		&.orange-style {
			background: linear-gradient(0deg, #FFFFFF, #FFFFFF),
				radial-gradient(53.72% 53.72% at 50% 50%, rgba(255, 255, 255, 0.5) 75.03%, rgba(255, 235, 216, 0.5) 100%)
				/* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */
			;

			border-radius: 32rpx;
			border: 2rpx solid #FC7631;
		}

		&.red-style {
			background: linear-gradient(0deg, #FFFFFF, #FFFFFF),
				radial-gradient(50% 50% at 50% 50%, rgba(255, 255, 255, 0.2) 83.9%, rgba(255, 216, 216, 0.2) 100%);

			border-radius: 32rpx;
			border: 2rpx solid var(--Accents-Red, rgba(255, 56, 60, 1))
		}

		.p-head {
			display: flex;
			justify-content: space-between;
			align-items: center;
			// margin-bottom: 20rpx;

			.p-info {
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: space-between;

				.dot-small {
					width: 10rpx;
					height: 10rpx;
					border-radius: 50%;
					margin-right: 12rpx;
				}

				.dot-small.orange {
					background: $color-orange;
				}

				.dot-small.red {
					background: $color-red;
				}

				.p-name {
					font-size: 28rpx;
					font-weight: bold;
					margin-right: 16rpx;
				}

				.p-tag {
					font-size: 28rpx;
					padding: 2rpx 10rpx;
					border-radius: 6rpx;

					&.orange-tag {
						color: $color-orange;
						background: rgba(250, 140, 22, 0.1);
					}

					&.red-tag {
						color: $color-red;
						background: rgba(255, 77, 79, 0.1);
					}
				}
			}

			.p-time {
				display: flex;
				align-items: center;
				font-weight: 400;
				font-size: 28rpx;
				color: #595959;

				.arrow-circle {
					width: 30rpx;
					height: 30rpx;
					background: #F0F0F0;
					border-radius: 50%;
					display: flex;
					align-items: center;
					justify-content: center;
					margin-left: 10rpx;
					font-size: 18rpx;
				}
			}
		}

		.p-metrics {
			margin-top: 32rpx;
			display: flex;
			justify-content: space-between;

			.metric {
				display: flex;
				flex-direction: column;
				align-items: center;

				.m-val {
					font-size: 32rpx;
					font-weight: 600;
					color: #333;
				}

				.m-lbl {
					font-size: 22rpx;
					color: #999;
					margin-top: 6rpx;
				}
			}
		}

		.p-desc {
			font-family: PingFang SC, PingFang SC;
			font-weight: 400;
			font-size: 28rpx;
			color: #2A2A2A;
		}

		.p-desc-row {
			display: flex;
			align-items: center;
			justify-content: space-between;
			margin-top: 26rpx;
			margin-bottom: 28rpx;
		}

		.p-divider {
			height: 0px;
			border: 2rpx solid #E4E1DD;
			margin-bottom: 28rpx;
		}

		/* 血糖波动曲线模块 */
		.sugar-chart-wrap {
			margin-top: 8rpx;

			.sugar-title {
				display: flex;
				align-items: center;
				justify-content: space-between;
				margin-bottom: 16rpx;

				.st {
					font-size: 26rpx;
					font-weight: 600;
					color: #333;
				}
				.st-legend {
					display: flex;
					align-items: center;
					font-size: 22rpx;
					color: #666;
				}
				.leg-dot {
					width: 16rpx;
					height: 16rpx;
					border-radius: 4rpx;
					margin-right: 6rpx;
					display: inline-block;
					vertical-align: middle;
				}
				.leg-dot.normal {
					background: rgba(0,180,42,0.25);
					border: 2rpx solid #00B42A;
				}
				.leg-dot.low {
					background: rgba(252,118,49,0.25);
					border: 2rpx solid #FC7631;
				}
			}

			.sugar-chart {
				position: relative;
				height: 260rpx;
				background: #FFFFFF;
				border-radius: 16rpx;
				padding: 24rpx 24rpx 36rpx;
				overflow: hidden;
				border: 1rpx solid #F1EDE7;
			}

			/* 区间底色：正常区(上部)占 2/3，偏低区(下部)占 1/3  */
			.range-normal {
				position: absolute;
				top: 10rpx; left: 24rpx; right: 24rpx;
				height: 66%;
				background: rgba(0,180,42,0.06);
				border-top-left-radius: 12rpx;
				border-top-right-radius: 12rpx;
			}
			.range-low {
				position: absolute;
				bottom: 36rpx; left: 24rpx; right: 24rpx;
				height: 34%;
				background: rgba(252,118,49,0.08);
				border-bottom-left-radius: 12rpx;
				border-bottom-right-radius: 12rpx;
			}
			/* 参考线 */
			.ref-line {
				position: absolute; left: 24rpx; right: 24rpx;
				height: 0; border-top: 2rpx dashed #CCC;
				.ref-txt {
					position: absolute;
					right: 4rpx;
					top: -18rpx;
					font-size: 18rpx;
					color: #888;
					background: #FFF;
					padding: 0 6rpx;
				}
			}
			.ref-hi { top: 10rpx; }
			.ref-low { top: 66%; }

			.sugar-svg {
				position: absolute;
				left: 24rpx;
				right: 24rpx;
				top: 24rpx;
				height: calc(100% - 60rpx);
				width: calc(100% - 48rpx);
				z-index: 2;
			}

			.x-axis {
				position: absolute;
				bottom: 6rpx; left: 24rpx; right: 24rpx;
				display: flex; justify-content: space-between;
				font-size: 20rpx; color: #999;
				z-index: 3;
			}

			.val-label {
				position: absolute;
				font-size: 20rpx; font-weight: 600; padding: 4rpx 12rpx;
				border-radius: 16rpx;
				z-index: 4;
				line-height: 1.2;
			}
			.val-label.start {
				top: 18rpx; left: 24rpx;
				background: rgba(0,180,42,0.15); color: #00B42A;
			}
			.val-label.mid {
				bottom: 36rpx; left: 50%;
				transform: translateX(-50%);
				background: rgba(245,63,63,0.15); color: #F53F3F;
			}
			.val-label.end {
				top: 18rpx; right: 24rpx;
				background: rgba(0,180,42,0.15); color: #00B42A;
			}

			/* 折线动态描边动画 */
			.sugar-line {
				stroke-dasharray: 1500; stroke-dashoffset: 1500;
				transition: stroke-dashoffset 1.8s cubic-bezier(.2,.7,.2,1);
			}
			.sugar-line.draw { stroke-dashoffset: 0; }
			.sugar-area { opacity: 0; transition: opacity .7s ease 1.2s; }
			.sugar-area.draw { opacity: 1; }

			/* 体征前后对比 */
			.cmp-row {
				display: flex; align-items: stretch; gap: 12rpx;
				margin-top: 24rpx;
			}
			.cmp-col {
				flex: 1; border-radius: 18rpx; padding: 20rpx 16rpx;
				&.before {
					background: linear-gradient(180deg, rgba(245,63,63,0.06) 0%, #FFF 100%);
					border: 2rpx solid rgba(245,63,63,0.2);
				}
				&.after {
					background: linear-gradient(180deg, rgba(0,180,42,0.06) 0%, #FFF 100%);
					border: 2rpx solid rgba(0,180,42,0.2);
				}
			}
			.cmp-tag {
				display: flex; align-items: center; gap: 8rpx;
				font-size: 22rpx; color: #475467; font-weight: 500;
				margin-bottom: 14rpx;
				.c-dot { width: 12rpx; height: 12rpx; border-radius: 50%; }
				.c-dot.red { background: #F53F3F; box-shadow: 0 0 0 3rpx rgba(245,63,63,.18); }
				.c-dot.green { background: #00B42A; box-shadow: 0 0 0 3rpx rgba(0,180,42,.18); }
			}
			.cmp-arrow {
				width: 48rpx; flex-shrink: 0;
				display: flex; flex-direction: column; align-items: center; justify-content: center;
				color: #CBD2DA; font-size: 32rpx; font-weight: 700;
				gap: 10rpx;
				.ca-gel {
					font-size: 18rpx; font-weight: 500; color: #FF7B52;
					background: rgba(255,123,82,0.12);
					border: 1rpx solid rgba(255,123,82,0.3);
					padding: 4rpx 10rpx; border-radius: 16rpx;
					white-space: nowrap;
				}
			}
			.cmp-items {
				.ci-item {
					text-align: center; background: #FFF; border-radius: 14rpx;
					padding: 14rpx 10rpx; margin-bottom: 10rpx;
					box-shadow: 0 4rpx 12rpx rgba(0,0,0,.04);
					.ci-num { font-size: 44rpx; font-weight: 700; color: #F53F3F; display: block; line-height: 1.1; }
					.ci-num.ok { color: #00B42A; }
					.ci-unit { font-size: 20rpx; color: #6B7280; display: block; margin-top: 2rpx; }
					.ci-label { font-size: 20rpx; color: #98A2B3; display: block; margin-top: 2rpx; }
				}
				.ci-row {
					display: flex; gap: 8rpx; margin-bottom: 8rpx;
					.ci-sm {
						flex: 1; text-align: center; background: #FFF;
						border-radius: 10rpx; padding: 10rpx 6rpx;
						box-shadow: 0 4rpx 12rpx rgba(0,0,0,.03);
						.cs-num { font-size: 26rpx; font-weight: 600; color: #1B1E23; display: block; }
						.cs-label { font-size: 18rpx; color: #98A2B3; display: block; margin-top: 2rpx; }
					}
				}
			}

			.goto-sugar {
				margin-top: 24rpx;
				background: linear-gradient(90deg, #FFF1E6 0%, #FFE3D0 100%);
				border: 2rpx solid rgba(255,120,70,0.3);
				color: #FC5A1D;
				font-size: 28rpx;
				font-weight: 600;
				padding: 20rpx 28rpx;
				border-radius: 44rpx;
				display: flex;
				align-items: center;
				justify-content: space-between;

				.arrow {
					font-size: 40rpx;
					line-height: 1;
					margin-top: -4rpx;
				}
			}
		}
	}

	/* --- 2. 应急处理 --- */
	.filter-wrap {
		padding: 30rpx 30rpx 10rpx;
	}

	.filter-pill {
		display: inline-block;
		background: #FC7631;
		color: #FFF;
		font-size: 24rpx;
		padding: 8rpx 24rpx;
		border-radius: 16rpx;
		margin-bottom: 28rpx;
	}

	.emergency-item {
		padding: 30rpx;

		.e-top {
			display: flex;
			align-items: center;
			margin-bottom: 20rpx;

			.tag-outline {
				font-size: 20rpx;
				padding: 2rpx 10rpx;
				border-radius: 6rpx;
				border: 1px solid transparent;
				margin-right: 12rpx;

				&.red {
					color: $color-red;
					border-color: $color-red;
				}

				&.orange {
					color: $color-orange;
					border-color: $color-orange;
				}
			}

			.e-title {
				font-size: 30rpx;
				font-weight: 600;
				flex: 1;
			}

			.e-status {
				font-size: 24rpx;
				font-weight: 500;
			}

			.e-status.red {
				color: $color-red;
			}

			.e-status.gray {
				color: #999;
			}
		}

		.e-desc {
			font-size: 26rpx;
			color: #666;
			line-height: 1.5;
			margin-bottom: 20rpx;
		}

		.e-action .btn-outline-orange {
			display: inline-flex;
			justify-content: center;
			align-items: center;
			width: 160rpx;
			height: 56rpx;
			font-size: 24rpx;
			color: $brand-orange;
			border: 2rpx solid $brand-orange;
			border-radius: 28rpx;
		}

		.e-footer {
			font-size: 24rpx;
			color: #999;
		}
	}

	.divider-line {
		height: 1rpx;
		background-color: #E4E1DD;
		margin: 0 30rpx;
	}

	$brand-orange: #FF5A26;
	$brand-orange-grad: linear-gradient(135deg, #FF7B47 0%, #FF4D1A 100%);
	$text-main: #222222;
	$text-sub: #666666;
	$text-gray: #999999;
	$color-green: #00B42A;
	$color-red: #F53F3F;

	/* ================= 1. 今日行程 样式 ================= */
	.schedule-section {
		position: relative;
		margin-bottom: 36rpx;
		margin: 32rpx;

		.schedule-header {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 24rpx;
			padding: 0 8rpx;

			.sh-left {
				display: flex;
				align-items: center;
				gap: 14rpx;

				.icon-orange-sq {
					width: 36rpx;
					height: 36rpx;
					background: $brand-orange;
					border-radius: 8rpx;
					display: flex;
					align-items: center;
					justify-content: center;

					.sq-txt {
						font-size: 20rpx;
						color: #FFF;
						font-weight: bold;
					}
				}

				.sh-title {
					font-family: Source Han Sans CN, Source Han Sans CN;
					font-weight: 500;
					font-size: 32rpx;
					color: #2A2A2A;
				}

				.sh-sub {
					font-weight: 400;
					font-size: 32rpx;
					color: #595959;
					margin-left: 8rpx;
				}
			}

			.sh-arrow-btn {
				width: 44rpx;
				height: 44rpx;
				background: rgba(255, 255, 255, 0.2);
				border-radius: 50%;
				display: flex;
				align-items: center;
				justify-content: center;

				.arrow-up {
					width: 14rpx;
					height: 14rpx;
					border-top: 3rpx solid #FFF;
					border-left: 3rpx solid #FFF;
					transform: rotate(45deg);
					margin-top: 4rpx;
				}
			}
		}

		.itinerary-wrapper {
			position: relative;
			display: flex;
			flex-direction: column;
			gap: 20rpx;

			/* 行程单行 (双盒排版) */
			.itinerary-row {
				display: flex;
				gap: 16rpx;
				align-items: stretch;

				/* 左侧图标盒 */
				.icon-box {
					width: 120rpx;
					height: 120rpx;
					background: #FFFFFF;
					border-radius: 32rpx;
					display: flex;
					align-items: center;
					justify-content: center;
					flex-shrink: 0;

					&.active-box {
						background: rgba(252, 118, 49, 0.1);
						border: 1px solid rgba(252, 118, 49, 0.1);
					}
				}

				/* 右侧信息盒 */
				.card-box {
					flex: 1;
					height: 120rpx;
					background: #FFFFFF;
					border-radius: 28rpx;
					padding: 20rpx 28rpx;
					display: flex;
					flex-direction: column;
					justify-content: space-between;
					box-sizing: border-box;

					&.active-card {
						background: rgba(252, 118, 49, 0.1);
						border: 1px solid rgba(252, 118, 49, 0.1);
					}

					.card-top {
						display: flex;
						justify-content: space-between;
						align-items: center;

						.title {
							font-size: 30rpx;
							font-weight: bold;
							color: $text-main;
						}

						.time {
							font-size: 24rpx;
							color: $text-sub;
						}

						.orange-txt {
							color: #FF7E53;
						}

						.orange-sub-txt {
							color: #A66B53;
						}
					}

					.card-bottom {
						display: flex;
						align-items: center;
						gap: 6rpx;

						.loc-pin {
							width: 28rpx;
							height: 28rpx;
						}

						.loc-name {
							font-size: 24rpx;
							color: $text-sub;
						}
					}
				}

				/* 节点 5 渐隐样式 */
				&.fade-row {
					opacity: 0.5;
				}
			}

			/* 展开蒙层与 Pill 按钮 */
			.expand-overlay {
				position: absolute;
				bottom: 0;
				left: 0;
				right: 0;
				height: 180rpx;
				// background: #FFF;
				display: flex;
				justify-content: center;
				align-items: flex-end;
				padding-bottom: 20rpx;
				border-bottom-left-radius: 28rpx;
				border-bottom-right-radius: 28rpx;

				.expand-pill-btn {
					background: #FFFFFF;
					padding: 14rpx 36rpx;
					border-radius: 40rpx;
					display: flex;
					align-items: center;
					gap: 10rpx;
					box-shadow: 0 6rpx 20rpx rgba(0, 0, 0, 0.15);

					.btn-txt {
						font-weight: 500;
						font-size: 32rpx;
						color: #FC7631;
					}

					.arrow-down-orange {
						width: 14rpx;
						height: 14rpx;
						border-bottom: 4rpx solid $brand-orange;
						border-right: 4rpx solid $brand-orange;
						transform: rotate(45deg);
						margin-bottom: 4rpx;
					}
				}
			}
		}
	}

	/* 纯 CSS 图标定义 */
	.custom-icon {
		width: 44rpx;
		height: 44rpx;
		position: relative;

		&.mountain-orange {
			border: 4rpx solid #FF7E53;
			border-radius: 8rpx;

			&::after {
				content: '';
				position: absolute;
				bottom: 4rpx;
				left: 6rpx;
				width: 0;
				height: 0;
				border-left: 12rpx solid transparent;
				border-right: 12rpx solid transparent;
				border-bottom: 20rpx solid #FF7E53;
			}
		}

		&.mountain-dark {
			border: 4rpx solid #333;
			border-radius: 8rpx;

			&::after {
				content: '';
				position: absolute;
				bottom: 4rpx;
				left: 6rpx;
				width: 0;
				height: 0;
				border-left: 12rpx solid transparent;
				border-right: 12rpx solid transparent;
				border-bottom: 20rpx solid #333;
			}
		}

		&.food-icon {
			&::before {
				content: '🍴';
				font-size: 36rpx;
				line-height: 44rpx;
			}
		}

		&.plane-icon {
			&::before {
				content: '✈';
				font-size: 36rpx;
				color: #888;
				line-height: 44rpx;
			}
		}
	}


	/* ================= 2. 服务台账 样式 ================= */
	.ledger-card-section {
		background: linear-gradient(180deg, #FFEBDD 0%, #FFFFFF 20%, #FFFFFF 100%);
		border-radius: 36rpx;
		padding: 32rpx 28rpx;
		margin: 32rpx;

		.ledger-header {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 28rpx;

			.lh-left {
				display: flex;
				align-items: center;
				gap: 12rpx;

				.icon-book-mark {
					width: 26rpx;
					height: 34rpx;
					border: 4rpx solid #222;
					border-radius: 4rpx;
					position: relative;

					&::after {
						content: '';
						position: absolute;
						top: 6rpx;
						left: 4rpx;
						width: 14rpx;
						height: 4rpx;
						background: #222;
						box-shadow: 0 8rpx 0 #222;
					}
				}

				.lh-title {
					font-size: 34rpx;
					font-weight: bold;
					color: $text-main;
				}
			}

			.lh-add-btn {
				background: #FFE3D6;
				padding: 8rpx 24rpx;
				border-radius: 30rpx;
				display: flex;
				align-items: center;
				gap: 6rpx;

				.plus-symbol {
					font-size: 28rpx;
					color: $brand-orange;
					font-weight: bold;
				}

				.add-txt {
					font-size: 26rpx;
					font-weight: bold;
					color: $brand-orange;
				}
			}
		}

		.record-list {
			display: flex;
			flex-direction: column;
			gap: 24rpx;

			.record-item {
				background: #FFFFFF;
				border: 1rpx solid #EAECEF;
				border-radius: 28rpx;
				padding: 28rpx;

				.ri-top {
					display: flex;
					align-items: center;
					margin-bottom: 16rpx;

					.ri-title {
						font-size: 30rpx;
						font-weight: bold;
						color: $text-main;
						margin-right: 16rpx;
					}

					.user-pill-tag {
						font-size: 22rpx;
						color: #555555;
						background: #EBECEF;
						padding: 4rpx 16rpx;
						border-radius: 20rpx;
						margin-right: auto;
					}

					.status-pill-tag {
						font-size: 22rpx;
						font-weight: 500;
						padding: 4rpx 16rpx;
						border-radius: 10rpx;

						&.tag-green {
							color: $color-green;
							background: #E6F9EE;
						}

						&.tag-red {
							color: $color-red;
							background: #FFE8E8;
						}
					}
				}

				.ri-desc {
					font-size: 26rpx;
					color: $text-sub;
					line-height: 1.6;
					display: block;
					margin-bottom: 20rpx;
					text-align: justify;
				}

				.ri-footer {
					font-size: 24rpx;
					color: $text-gray;
				}

				.ri-action {
					.btn-handle-orange {
						display: inline-block;
						background: $brand-orange-grad;
						color: #FFFFFF;
						font-size: 26rpx;
						font-weight: bold;
						height: 58rpx;
						line-height: 58rpx;
						padding: 0 36rpx;
						border-radius: 30rpx;
						margin: 0;
						box-shadow: 0 4rpx 12rpx rgba(255, 90, 38, 0.25);
					}
				}
			}
		}
	}

	.safe-bottom {
		height: 60rpx;
	}
</style>