<template>
	<view class="page-container">
		<view class="top-gradient"></view>

		<!-- 顶部返回栏 -->
		<view class="nav-bar">
			<view class="nav-back" @click="goBack">
				<text class="arrow">‹</text>
				<text>返回</text>
			</view>
			<text class="nav-title">血糖恢复正常方案</text>
			<view style="width: 100rpx;"></view>
		</view>

		<!-- 患者基本信息 -->
		<view class="profile-card">
			<view class="pf-left">
				<view class="avatar">张</view>
				<view class="pf-info">
					<text class="pf-name">张爷爷</text>
					<text class="pf-sub">男 · 76岁 · 团内游客</text>
				</view>
			</view>
			<view class="pf-status">
				<view class="dot low"></view>
				<text>血糖偏低</text>
			</view>
		</view>

		<!-- 恢复总览：当前值 + 动画回正条 -->
		<view class="summary-card">
			<view class="sm-head">
				<text class="sm-title">当前血糖</text>
				<text class="sm-time">10:30 检测</text>
			</view>
			<view class="sm-row">
				<view class="sm-num-wrap">
					<text class="sm-num">3.6</text>
					<text class="sm-unit">mmol/L</text>
				</view>
				<view class="sm-tag low-tag">偏低</view>
			</view>
			<!-- 恢复进度：处理中→已恢复的动态条 -->
			<view class="recover-bar">
				<view class="rb-bg">
					<view class="rb-fill" :style="{ width: progress + '%' }"></view>
					<view class="rb-pin" :style="{ left: progress + '%' }">
						<text v-if="progress >= 100" class="pin-ok">✓</text>
					</view>
				</view>
				<view class="rb-labels">
					<text>3.6</text>
					<text class="target">目标：4.8</text>
					<text>6.1</text>
				</view>
			</view>
			<view class="recover-status">
				<text class="rs-txt">恢复进度 {{ progress }}%</text>
				<text v-if="progress < 100" class="rs-sub">{{ phaseText }}</text>
				<text v-else class="rs-sub ok">已恢复至正常区间</text>
			</view>
		</view>

		<!-- 血糖波动动态图 -->
		<view class="chart-card">
			<view class="card-head">
				<view>
					<text class="ch-title">血糖波动趋势图</text>
					<text class="ch-sub">实时绘制 · 干预前后对比</text>
				</view>
				<view class="legend">
					<view class="legend-item"><view class="li-dot before"></view><text>处理前</text></view>
					<view class="legend-item"><view class="li-dot after"></view><text>处理后</text></view>
				</view>
			</view>

			<view class="chart-area">
				<!-- Y 轴刻度 -->
				<view class="y-axis">
					<text>7.0</text>
					<text>6.1</text>
					<text>4.5</text>
					<text>3.9</text>
					<text>3.0</text>
				</view>

				<view class="chart-inner">
					<!-- 区间带：偏低 + 正常 -->
					<view class="band band-low"></view>
					<view class="band band-normal"></view>
					<!-- 参考横线 -->
					<view class="ref-line ref-low"></view>
					<view class="ref-line ref-high"></view>

					<svg viewBox="0 0 500 200" preserveAspectRatio="none" class="sugar-svg">
						<defs>
							<linearGradient id="sugarFill" x1="0" y1="0" x2="0" y2="1">
								<stop offset="0%" stop-color="#FF8A65" stop-opacity="0.35" />
								<stop offset="100%" stop-color="#FF8A65" stop-opacity="0" />
							</linearGradient>
							<linearGradient id="sugarLine" x1="0" y1="0" x2="1" y2="0">
								<stop offset="0%" stop-color="#4CAF50" />
								<stop offset="48%" stop-color="#FF5252" />
								<stop offset="100%" stop-color="#4CAF50" />
							</linearGradient>
						</defs>

						<!-- 面积填充 -->
						<path
							class="sugar-area"
							:class="{ draw: chartAnim }"
							d="M 20 55 L 80 60 L 140 88 L 200 120 L 250 155 L 310 130 L 370 108 L 440 95 L 480 88 L 480 200 L 20 200 Z"
							fill="url(#sugarFill)"
						/>
						<!-- 主折线：5.2 → 低点3.6 → 4.8 -->
						<path
							class="sugar-line"
							:class="{ draw: chartAnim }"
							d="M 20 55 L 80 60 L 140 88 L 200 120 L 250 155 L 310 130 L 370 108 L 440 95 L 480 88"
							fill="none"
							stroke="url(#sugarLine)"
							stroke-width="3.5"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<!-- 起点：正常 5.2 -->
						<circle
							class="sv-point p-start"
							:class="{ show: chartAnim }"
							cx="20" cy="55" r="5.5"
							fill="#4CAF50"
							stroke="#fff" stroke-width="2"
						/>
						<!-- 低谷点 3.6 -->
						<circle
							class="sv-point p-mid"
							:class="{ show: chartAnim }"
							cx="250" cy="155" r="6.5"
							fill="#FF5252"
							stroke="#fff" stroke-width="2.5"
						/>
						<!-- 终点：恢复后 4.8 -->
						<circle
							class="sv-point p-end"
							:class="{ show: chartAnim }"
							cx="480" cy="88" r="6.5"
							fill="#4CAF50"
							stroke="#fff" stroke-width="2.5"
						/>
					</svg>

					<!-- X 轴标签 -->
					<view class="x-axis">
						<text>10:00<br /><text class="xa-sub">正常 5.2</text></text>
						<text>10:15</text>
						<text class="xa-mid">10:30<br /><text class="xa-sub">预警 3.6</text></text>
						<text>10:45</text>
						<text>11:00<br /><text class="xa-sub ok">恢复 4.8</text></text>
					</view>
				</view>
			</view>
		</view>

		<!-- 体征前后对比 -->
		<view class="compare-card">
			<view class="card-head">
				<text class="ch-title">体征数据 · 前后对比</text>
				<text class="ch-sub">处理前 vs 恢复后</text>
			</view>

			<view class="compare-wrap">
				<!-- 处理前 -->
				<view class="cmp-col before">
					<view class="cmp-head">
						<view class="ch-dot red"></view>
						<text>处理前（低血糖状态）</text>
					</view>
					<view class="cmp-metrics">
						<view class="metric">
							<text class="m-num danger">3.6</text>
							<text class="m-unit">mmol/L</text>
							<text class="m-label">血糖</text>
						</view>
						<view class="metric-row">
							<view class="m-item">
								<text class="mi-num">76</text>
								<text class="mi-label">心率</text>
							</view>
							<view class="m-item">
								<text class="mi-num">120/78</text>
								<text class="mi-label">血压</text>
							</view>
						</view>
						<view class="metric-row">
							<view class="m-item">
								<text class="mi-num">96%</text>
								<text class="mi-label">血氧</text>
							</view>
							<view class="m-item">
								<text class="mi-num">36.5°</text>
								<text class="mi-label">体温</text>
							</view>
						</view>
					</view>
				</view>

				<!-- 箭头分隔 -->
				<view class="cmp-arrow" :class="{ anim: chartAnim }">
					<view class="ca-gel">补糖凝胶</view>
					<text>→</text>
				</view>

				<!-- 恢复后 -->
				<view class="cmp-col after">
					<view class="cmp-head">
						<view class="ch-dot green"></view>
						<text>恢复后（正常区间）</text>
					</view>
					<view class="cmp-metrics">
						<view class="metric">
							<text class="m-num ok">4.8</text>
							<text class="m-unit">mmol/L</text>
							<text class="m-label">血糖</text>
						</view>
						<view class="metric-row">
							<view class="m-item">
								<text class="mi-num">72</text>
								<text class="mi-label">心率</text>
							</view>
							<view class="m-item">
								<text class="mi-num">122/78</text>
								<text class="mi-label">血压</text>
							</view>
						</view>
						<view class="metric-row">
							<view class="m-item">
								<text class="mi-num">96%</text>
								<text class="mi-label">血氧</text>
							</view>
							<view class="m-item">
								<text class="mi-num">36.5°</text>
								<text class="mi-label">体温</text>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>

		<!-- 处理步骤（带打卡完成态） -->
		<view class="steps-card">
			<view class="card-head">
				<text class="ch-title">恢复处理步骤</text>
				<text class="ch-sub">4 步 紧急干预方案</text>
			</view>

			<view class="step-list">
				<view class="step-item" :class="{ done: stepDone[0] }" @click="toggleStep(0)">
					<view class="si-icon">🍬</view>
					<view class="si-body">
						<view class="si-head">
							<text class="si-title">1. 立即补充糖分</text>
							<view class="si-check">{{ stepDone[0] ? '✓ 已执行' : '待执行' }}</view>
						</view>
						<text class="si-desc">口服 15g 快速碳水：方糖 3~4 块、半杯甜果汁、或一勺蜂蜜。避免含脂肪的糖果（吸收慢）。</text>
						<view class="si-tips">建议 15 分钟后复测血糖</view>
					</view>
				</view>

				<view class="step-item" :class="{ done: stepDone[1] }" @click="toggleStep(1)">
					<view class="si-icon">📏</view>
					<view class="si-body">
						<view class="si-head">
							<text class="si-title">2. 静坐休息并监测</text>
							<view class="si-check">{{ stepDone[1] ? '✓ 已执行' : '待执行' }}</view>
						</view>
						<text class="si-desc">让老人就地坐下或侧卧，避免走动跌倒。随行医护持续监测心率、出汗、意识状态。</text>
					</view>
				</view>

				<view class="step-item" :class="{ done: stepDone[2] }" @click="toggleStep(2)">
					<view class="si-icon">🧪</view>
					<view class="si-body">
						<view class="si-head">
							<text class="si-title">3. 复测并二次补充</text>
							<view class="si-check">{{ stepDone[2] ? '✓ 已执行' : '待执行' }}</view>
						</view>
						<text class="si-desc">15 分钟后复测：若仍 < 3.9 mmol/L，再口服 15g 糖分；连续 2 次不回升需启动第 4 步。</text>
					</view>
				</view>

				<view class="step-item" :class="{ done: stepDone[3] }" @click="toggleStep(3)">
					<view class="si-icon">🚑</view>
					<view class="si-body">
						<view class="si-head">
							<text class="si-title">4. 应急联络与就医</text>
							<view class="si-check">{{ stepDone[3] ? '✓ 已执行' : '待执行' }}</view>
						</view>
						<text class="si-desc">老人出现意识模糊、抽搐、复测不回升：立即拨打 120，并通知家属及随行医生，保持呼吸道通畅。</text>
						<view class="btn-row">
							<view class="mini-btn phone">📞 通知家属</view>
							<view class="mini-btn call">🚨 呼叫 120</view>
						</view>
					</view>
				</view>
			</view>
		</view>

		<!-- 底部 CTA -->
		<view class="footer-cta">
			<button class="cta-btn" :class="{ ok: allDone }" @click="markRecovered">
				{{ allDone ? '✓ 已恢复至正常区间' : '确认已恢复并记录' }}
			</button>
		</view>

		<view class="safe-bottom"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 四步处理的勾选状态
				stepDone: [false, false, false, false],
				// 血糖趋势图动画开关
				chartAnim: false
			};
		},
		mounted() {
			// 页面打开 300ms 后开始绘制折线动画
			this.animTimer = setTimeout(() => {
				this.chartAnim = true;
			}, 300);
		},
		beforeDestroy() {
			if (this.animTimer) clearTimeout(this.animTimer);
		},
		computed: {
			doneCount() {
				return this.stepDone.filter(v => v).length;
			},
			progress() {
				// 进度：每步 25%；全部完成后额外给"恢复确认"拉到 100%
				const base = this.doneCount * 25;
				return Math.min(100, base);
			},
			phaseText() {
				if (this.doneCount === 0) return '等待启动干预措施';
				if (this.doneCount < 4) return `正在执行第 ${this.doneCount + 1} 步…`;
				return '处理步骤已完成，等待确认血糖回正';
			},
			allDone() {
				return this.doneCount === 4;
			}
		},
		methods: {
			goBack() {
				uni.navigateBack({ delta: 1 });
			},
			toggleStep(idx) {
				const arr = this.stepDone.slice();
				arr[idx] = !arr[idx];
				this.stepDone = arr;
			},
			markRecovered() {
				if (!this.allDone) {
					uni.showToast({ title: '请先完成全部 4 步处理', icon: 'none' });
					return;
				}
				uni.showToast({ title: '已记录：血糖恢复正常', icon: 'success' });
			}
		}
	};
</script>

<style lang="scss" scoped>
	.page-container {
		min-height: 100vh;
		background: #F7F8FA;
		padding-bottom: 40rpx;
		position: relative;
	}

	.top-gradient {
		position: absolute;
		top: 0; left: 0; right: 0; height: 460rpx;
		background: linear-gradient(180deg, #FFE3D1 0%, #F7F8FA 100%);
		z-index: 0;
	}

	.nav-bar {
		position: relative; z-index: 1;
		display: flex; align-items: center; justify-content: space-between;
		padding: 80rpx 32rpx 20rpx;

		.nav-back {
			display: flex; align-items: center; font-size: 28rpx; color: #2A2A2A;
			.arrow { font-size: 40rpx; margin-right: 4rpx; line-height: 1; }
		}
		.nav-title {
			font-size: 32rpx; font-weight: 600; color: #111;
		}
	}

	/* 患者卡 */
	.profile-card {
		position: relative; z-index: 1;
		margin: 16rpx 32rpx 24rpx;
		padding: 28rpx;
		border-radius: 28rpx;
		background: #FFFFFF;
		display: flex; align-items: center; justify-content: space-between;
		box-shadow: 0 8rpx 20rpx rgba(0,0,0,0.03);

		.pf-left {
			display: flex; align-items: center;
			.avatar {
				width: 88rpx; height: 88rpx; border-radius: 50%;
				background: linear-gradient(135deg, #FF8B5C 0%, #F55C2E 100%);
				color: #FFF; font-size: 36rpx; font-weight: bold;
				display: flex; align-items: center; justify-content: center;
				margin-right: 20rpx;
			}
			.pf-info { display: flex; flex-direction: column; }
			.pf-name { font-size: 34rpx; font-weight: 600; color: #111; }
			.pf-sub { font-size: 24rpx; color: #888; margin-top: 6rpx; }
		}
		.pf-status {
			display: flex; align-items: center; gap: 8rpx;
			background: #FFF1EA; padding: 10rpx 22rpx; border-radius: 32rpx;
			font-size: 24rpx; color: #F53F3F; font-weight: 500;
			.dot { width: 12rpx; height: 12rpx; border-radius: 50%; background: #F53F3F; }
			.dot.low { background: #F53F3F; }
		}
	}

	/* 总览卡 */
	.summary-card {
		position: relative; z-index: 1;
		margin: 0 32rpx 24rpx;
		padding: 32rpx;
		border-radius: 28rpx;
		background: linear-gradient(135deg, #FFFFFF 0%, #FFF5EE 100%);
		box-shadow: 0 8rpx 20rpx rgba(255,110,60,0.08);
		border: 2rpx solid rgba(255,110,60,0.15);

		.sm-head { display: flex; justify-content: space-between; align-items: center; }
		.sm-title { font-size: 26rpx; color: #555; font-weight: 500; }
		.sm-time { font-size: 22rpx; color: #999; }

		.sm-row { display: flex; align-items: baseline; margin-top: 16rpx; }
		.sm-num { font-size: 84rpx; font-weight: 800; color: #F53F3F; line-height: 1; }
		.sm-unit { font-size: 28rpx; color: #F53F3F; margin-left: 10rpx; font-weight: 600; }
		.sm-tag {
			margin-left: auto;
			background: #FFE1D0; color: #F53F3F;
			font-size: 24rpx; font-weight: 600;
			padding: 8rpx 20rpx; border-radius: 16rpx;
		}
	}

	/* 恢复进度条 */
	.recover-bar {
		margin-top: 36rpx;
		.rb-bg {
			position: relative;
			height: 20rpx;
			background: #F0EEE9;
			border-radius: 10rpx;
			overflow: visible;
		}
		.rb-fill {
			position: absolute; top: 0; left: 0;
			height: 100%;
			background: linear-gradient(90deg, #F53F3F 0%, #FF7A3D 60%, #00B42A 100%);
			border-radius: 10rpx;
			transition: width .6s ease;
		}
		.rb-pin {
			position: absolute; top: 50%;
			width: 36rpx; height: 36rpx;
			border-radius: 50%;
			background: #FFFFFF;
			transform: translate(-50%, -50%);
			box-shadow: 0 4rpx 10rpx rgba(0,0,0,0.15);
			display: flex; align-items: center; justify-content: center;
			transition: left .6s ease;
		}
		.pin-ok { font-size: 24rpx; color: #00B42A; font-weight: bold; }

		.rb-labels {
			display: flex; justify-content: space-between;
			margin-top: 12rpx;
			font-size: 22rpx; color: #999;
			.target { color: #FC7631; font-weight: 600; }
		}
	}

	.recover-status {
		margin-top: 20rpx;
		display: flex; justify-content: space-between; align-items: center;
		.rs-txt { font-size: 28rpx; color: #333; font-weight: 600; }
		.rs-sub { font-size: 24rpx; color: #999; }
		.rs-sub.ok { color: #00B42A; font-weight: 600; }
	}

	/* 步骤卡 */
	.steps-card {
		position: relative; z-index: 1;
		margin: 0 32rpx 24rpx;
		padding: 32rpx;
		border-radius: 28rpx;
		background: #FFFFFF;
		box-shadow: 0 8rpx 20rpx rgba(0,0,0,0.03);

		.card-head { display: flex; justify-content: space-between; align-items: center; margin-bottom: 24rpx; }
		.ch-title { font-size: 32rpx; font-weight: 700; color: #111; }
		.ch-sub { font-size: 24rpx; color: #999; }

		.step-list { display: flex; flex-direction: column; gap: 24rpx; }
		.step-item {
			display: flex;
			padding: 24rpx;
			border-radius: 20rpx;
			background: #FAFAF8;
			border: 2rpx solid #EFECE6;
			transition: all .2s ease;

			&.done {
				background: #F6FFED;
				border-color: rgba(0,180,42,0.25);
			}
			.si-icon {
				width: 80rpx; height: 80rpx;
				border-radius: 20rpx;
				background: #FFFFFF;
				display: flex; align-items: center; justify-content: center;
				font-size: 40rpx;
				margin-right: 20rpx;
				flex-shrink: 0;
				box-shadow: 0 4rpx 8rpx rgba(0,0,0,0.04);
			}
			.si-body { flex: 1; min-width: 0; }
			.si-head { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10rpx; }
			.si-title { font-size: 30rpx; font-weight: 700; color: #111; }
			.si-check {
				font-size: 22rpx; color: #F53F3F; font-weight: 600;
				background: #FFF0EE;
				padding: 4rpx 14rpx; border-radius: 12rpx;
			}
			.done .si-check { background: #E8FFE0; color: #00B42A; }
			.si-desc {
				font-size: 26rpx; color: #555; line-height: 1.6;
			}
			.si-tips {
				margin-top: 12rpx;
				font-size: 22rpx; color: #FC7631; font-weight: 500;
			}
			.btn-row { display: flex; gap: 16rpx; margin-top: 16rpx; flex-wrap: wrap; }
			.mini-btn {
				font-size: 24rpx; padding: 10rpx 22rpx;
				border-radius: 20rpx; font-weight: 600;
			}
			.mini-btn.phone { background: #FFF1EA; color: #FC7631; }
			.mini-btn.call { background: #FFECEC; color: #F53F3F; }
		}
	}

	/* 底部 CTA */
	.footer-cta {
		position: relative; z-index: 1;
		margin: 32rpx;
		.cta-btn {
			width: 100%;
			height: 96rpx;
			line-height: 96rpx;
			border-radius: 48rpx;
			font-size: 32rpx; font-weight: 700;
			background: linear-gradient(90deg, #FF7A3D 0%, #F53F3F 100%);
			color: #FFF;
			margin: 0;
			border: none;
			box-shadow: 0 8rpx 20rpx rgba(255,61,0,0.25);
			&::after { border: none; }
			&.ok { background: linear-gradient(90deg, #34C759 0%, #00B42A 100%); }
		}
	}
	.safe-bottom { height: 40rpx; }

	/* ============ 血糖波动趋势图 ============ */
	.chart-card {
		background: #FFFFFF;
		border-radius: 32rpx;
		padding: 32rpx;
		margin: 0 28rpx 28rpx;
		box-shadow: 0 8rpx 30rpx rgba(255,130,92,0.08);
		.card-head {
			display: flex; align-items: center; justify-content: space-between;
			margin-bottom: 24rpx;
			.ch-title { font-size: 34rpx; font-weight: 600; color: #1B1E23; }
			.ch-sub { font-size: 22rpx; color: #9BA4B1; margin-top: 6rpx; display: block; }
		}
		.legend { display: flex; gap: 24rpx;
			.legend-item { display: flex; align-items: center; gap: 10rpx;
				font-size: 22rpx; color: #6B7280;
				.li-dot { width: 16rpx; height: 16rpx; border-radius: 50%; }
				.li-dot.before { background: #FF5252; }
				.li-dot.after { background: #4CAF50; }
			}
		}
	}
	.chart-area {
		display: flex; gap: 14rpx;
		.y-axis {
			width: 72rpx; flex-shrink: 0;
			display: flex; flex-direction: column; justify-content: space-between;
			padding: 8rpx 0 52rpx;
			text { font-size: 20rpx; color: #9BA4B1; text-align: right; padding-right: 4rpx; }
		}
		.chart-inner {
			flex: 1; position: relative;
			height: 400rpx;
		}
		.band { position: absolute; left: 0; right: 0; z-index: 0; }
		.band-low {
			top: 62%; bottom: 0;
			background: linear-gradient(180deg, rgba(255,95,95,0.10) 0%, rgba(255,195,113,0.08) 100%);
			border-bottom-left-radius: 12rpx; border-bottom-right-radius: 12rpx;
		}
		.band-normal {
			top: 14%; height: 48%;
			background: linear-gradient(180deg, rgba(123,208,159,0.12) 0%, rgba(52,199,89,0.06) 100%);
		}
		.ref-line { position: absolute; left: 0; right: 0; height: 1rpx; z-index: 1;
			background: repeating-linear-gradient(90deg, #C7CDD4 0, #C7CDD4 6rpx, transparent 6rpx, transparent 12rpx);
		}
		.ref-low { top: 62%; }
		.ref-high { top: 14%; }
		.sugar-svg {
			position: absolute; inset: 0 0 72rpx 0;
			width: 100%; height: calc(100% - 72rpx);
			z-index: 2;
		}
		/* 折线绘制动画 */
		.sugar-line {
			stroke-dasharray: 1200; stroke-dashoffset: 1200;
			transition: stroke-dashoffset 2.4s cubic-bezier(.2,.7,.2,1);
		}
		.sugar-line.draw { stroke-dashoffset: 0; }
		.sugar-area { opacity: 0; transition: opacity .8s ease 1.6s; }
		.sugar-area.draw { opacity: 1; }

		/* 数据点动画 */
		.sv-point { opacity: 0; transform: scale(.3); }
		.sv-point.show { opacity: 1; transform: scale(1); transition: transform .3s cubic-bezier(.3,1.6,.6,1), opacity .3s; }
		.p-start.show { transition-delay: .1s; }
		.p-mid.show { transition-delay: .9s; }
		.p-end.show { transition-delay: 2.1s;
			animation: sugarPulse 1.8s ease-in-out 2.6s infinite;
		}
		@keyframes sugarPulse {
			0%,100% { filter: drop-shadow(0 0 0 rgba(76,175,80,.6)); }
			50% { filter: drop-shadow(0 0 8rpx rgba(76,175,80,.8)); }
		}

		/* X 轴时间标签 */
		.x-axis {
			position: absolute; left: 0; right: 0; bottom: 0; height: 72rpx;
			display: flex; justify-content: space-between; align-items: flex-start;
			padding-top: 8rpx;
			text { font-size: 20rpx; color: #6B7280; line-height: 1.25; text-align: center; }
			.xa-sub { font-size: 18rpx; color: #4CAF50; margin-top: 2rpx; display: block; }
			.xa-sub.ok { color: #34C759; }
			.xa-mid text.xa-sub { color: #FF8A3D; }
		}
	}

	/* ============ 体征前后对比 ============ */
	.compare-card {
		background: #FFFFFF;
		border-radius: 32rpx;
		padding: 32rpx;
		margin: 0 28rpx 28rpx;
		box-shadow: 0 8rpx 30rpx rgba(255,130,92,0.08);
		.card-head {
			display: flex; align-items: center; justify-content: space-between;
			margin-bottom: 28rpx;
			.ch-title { font-size: 34rpx; font-weight: 600; color: #1B1E23; }
			.ch-sub { font-size: 22rpx; color: #9BA4B1; }
		}
	}
	.compare-wrap {
		display: flex; align-items: stretch; gap: 16rpx;
	}
	.cmp-col {
		flex: 1; border-radius: 24rpx;
		padding: 24rpx 22rpx;
		.cmp-head {
			display: flex; align-items: center; gap: 10rpx;
			font-size: 24rpx; color: #475467; font-weight: 500;
			margin-bottom: 20rpx;
			.ch-dot { width: 14rpx; height: 14rpx; border-radius: 50%; }
			.ch-dot.red { background: #FF5252; box-shadow: 0 0 0 4rpx rgba(255,82,82,.18); }
			.ch-dot.green { background: #34C759; box-shadow: 0 0 0 4rpx rgba(52,199,89,.18); }
		}
	}
	.cmp-col.before {
		background: linear-gradient(180deg, rgba(255,82,82,0.08) 0%, rgba(255,255,255,1) 100%);
		border: 2rpx solid rgba(255,82,82,0.25);
	}
	.cmp-col.after {
		background: linear-gradient(180deg, rgba(52,199,89,0.08) 0%, rgba(255,255,255,1) 100%);
		border: 2rpx solid rgba(52,199,89,0.25);
	}
	.cmp-metrics {
		.metric {
			background: #FFFFFF;
			border-radius: 18rpx;
			padding: 18rpx 14rpx 16rpx;
			box-shadow: 0 4rpx 14rpx rgba(0,0,0,.05);
			text-align: center;
			margin-bottom: 14rpx;
			.m-num {
				display: block;
				font-size: 52rpx; font-weight: 700; line-height: 1.1;
				&.danger { color: #FF5252; }
				&.ok { color: #34C759; }
			}
			.m-unit { font-size: 22rpx; color: #6B7280; margin-top: 4rpx; display: block; }
			.m-label { font-size: 22rpx; color: #98A2B3; margin-top: 2rpx; display: block; }
		}
		.metric-row {
			display: flex; gap: 12rpx;
			margin-bottom: 12rpx;
			.m-item {
				flex: 1; background: #FFFFFF;
				border-radius: 14rpx;
				padding: 14rpx 10rpx;
				box-shadow: 0 4rpx 14rpx rgba(0,0,0,.04);
				text-align: center;
				.mi-num { display: block; font-size: 32rpx; font-weight: 600; color: #1B1E23; }
				.mi-label { display: block; font-size: 20rpx; color: #98A2B3; margin-top: 4rpx; }
			}
		}
	}
	.cmp-arrow {
		width: 56rpx; flex-shrink: 0;
		display: flex; flex-direction: column; align-items: center; justify-content: center;
		gap: 10rpx;
		color: #CBD2DA; font-size: 36rpx; font-weight: 700;
		transition: all .6s ease 2.4s;
		&.anim { color: #34C759; transform: scale(1.3); }
		.ca-gel {
			font-size: 18rpx; font-weight: 500; color: #FF7B52;
			background: rgba(255,123,82,0.12);
			border: 1rpx solid rgba(255,123,82,0.3);
			padding: 4rpx 10rpx; border-radius: 16rpx;
			white-space: nowrap;
		}
	}
</style>
