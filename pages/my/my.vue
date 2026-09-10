<template>
	<view class="page-container">
		<!-- 顶部环境渐变背景 -->
		<view class="ambient-gradient-bg"></view>

		<!-- 1. 顶部 Header (包含模拟微信右上角胶囊) -->
		<view class="header-section">
			<view class="title-wrapper">
				<text class="page-title">浪无忧</text>
				<text class="page-subtitle">导游端 · 银发团智能管家</text>
			</view>

		</view>

		<!-- 2. 黑金风格导游个人信息卡片 -->
		<view class="profile-card card-shadow">
			<!-- 头部个人基本信息 -->
			<view class="user-info-row">
				<image class="avatar" src="/static/my/p.jpg" mode="aspectFill" />
				<view class="user-detail">
					<view class="name-line">
						<!-- <text class="user-name">李明辉</text> -->
						<view class="role-pill">
							<text>导游</text>
							<text class="arrow">▾</text>
						</view>
					</view>
					<text class="user-sub">编号ZJ2020088</text>
				</view>
			</view>

			<!-- 角色切换区域 -->
			<view class="role-switch-panel">
				<text class="switch-title">切换查看角色</text>
				<view class="role-btn-group">
					<!-- 当前选中的导游角色 -->
					<view class="role-btn active">
						<text class="btn-icon"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"
								xmlns="http://www.w3.org/2000/svg">
								<path d="M2.3335 12.8333H3.50016H4.66683" stroke="white" stroke-width="2"
									stroke-linecap="round" stroke-linejoin="round" />
								<path d="M3.5 12.8333V1.16666" stroke="white" stroke-width="2" stroke-linecap="round"
									stroke-linejoin="round" />
								<path d="M11.6667 1.75H3.5V6.41667H11.6667L10.5 4.08333L11.6667 1.75Z" fill="white"
									stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
							</svg>
						</text>
						<text>导游</text>
					</view>
					<!-- 其他角色切换按纽 -->
					<view class="role-btn light">
						<text class="btn-icon orange-color"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"
								xmlns="http://www.w3.org/2000/svg">
								<rect opacity="0.01" width="14" height="14" fill="url(#paint0_linear_76_5039)" />
								<path fill-rule="evenodd" clip-rule="evenodd"
									d="M12.8386 1.88407C12.7803 1.65544 12.0617 1.35292 11.837 1.41202L11.6993 1.44858L11.0258 0.676787C11.0152 0.663567 10.9874 0.62994 10.9371 0.571384L11.0161 0.665686C10.9411 0.582072 10.5803 0.208881 10.3065 0.0480055C9.91458 -0.180629 6.87548 0.475716 6.48355 1.08775C6.31994 1.34843 6.24653 1.65196 6.21011 1.80253L6.20826 1.81017L5.96874 3.01245L5.83109 3.049C5.60557 3.1081 5.1343 3.7349 5.19264 3.96352C5.21972 4.07403 5.29071 4.1687 5.3892 4.22566C5.48769 4.28261 5.60516 4.29692 5.71444 4.26526L6.62897 4.02262C6.84672 5.20234 7.86933 6.09432 9.09494 6.09432C10.4807 6.09432 11.6044 4.95893 11.6044 3.55759C11.6044 3.26285 11.5539 2.97513 11.4598 2.70993L12.5337 2.41443C12.6445 2.38457 12.7389 2.3119 12.7961 2.21242C12.8532 2.11295 12.8685 1.99483 12.8386 1.88407ZM11.0161 0.665686L11.0172 0.667033C11.0311 0.684197 11.0352 0.688495 11.0258 0.676787L11.0173 0.667027C11.0169 0.666589 11.0165 0.666142 11.0161 0.665686ZM10.7058 9.04398C10.4881 9.04398 10.2851 9.0883 10.0962 9.16919C10.0895 9.16213 10.0842 9.15507 10.079 9.1481L10.079 9.14808C10.0733 9.14046 10.0677 9.13294 10.0604 9.12564L6.18609 5.20933C5.93132 4.95101 5.55603 4.85205 5.20701 4.95115L5.20001 4.94415C5.19665 4.94752 5.19149 4.94927 5.18626 4.95104C5.18061 4.95295 5.17488 4.95489 5.17124 4.95893C5.03955 4.99883 4.91805 5.06675 4.81507 5.15801C2.43621 6.61069 0.803896 10.1133 0.803896 13.0116C0.803896 13.1563 0.796551 13.2739 0.789734 13.383C0.777468 13.5793 0.766909 13.7483 0.803896 13.9992H8.26088V10.1801L8.63104 10.5557C8.69637 10.6219 8.76169 10.674 8.83402 10.7183C8.86754 11.0869 9.17471 11.3702 9.54479 11.3738C9.88826 11.3731 10.1832 11.1293 10.2486 10.7922H10.2633V10.6444C10.2633 10.401 10.4593 10.2089 10.6911 10.2089C10.9306 10.2089 11.1196 10.408 11.1196 10.6444V13.9992H12.2658V10.6444C12.2752 10.2241 12.1152 9.81776 11.8218 9.51673C11.5284 9.21571 11.1262 9.04534 10.7058 9.04398Z"
									fill="url(#paint1_linear_76_5039)" />
								<defs>
									<linearGradient id="paint0_linear_76_5039" x1="4.2" y1="3.5" x2="12.6" y2="16.1"
										gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint1_linear_76_5039" x1="4.4009" y1="3.50091" x2="13.2054"
										y2="14.8938" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
								</defs>
							</svg>
						</text>
						<text class="orange-color">老年游客</text>
					</view>
					<view class="role-btn light">
						<text class="btn-icon orange-color"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"
								xmlns="http://www.w3.org/2000/svg">
								<path
									d="M4.08333 9.91667C4.88875 9.91667 5.54167 9.26375 5.54167 8.45833C5.54167 7.65292 4.88875 7 4.08333 7C3.27792 7 2.625 7.65292 2.625 8.45833C2.625 9.26375 3.27792 9.91667 4.08333 9.91667Z"
									fill="url(#paint0_linear_76_5048)" stroke="url(#paint1_linear_76_5048)"
									stroke-linecap="round" stroke-linejoin="round" />
								<path
									d="M9.91683 9.91667C10.7222 9.91667 11.3752 9.26375 11.3752 8.45833C11.3752 7.65292 10.7222 7 9.91683 7C9.11141 7 8.4585 7.65292 8.4585 8.45833C8.4585 9.26375 9.11141 9.91667 9.91683 9.91667Z"
									fill="url(#paint2_linear_76_5048)" stroke="url(#paint3_linear_76_5048)"
									stroke-linecap="round" stroke-linejoin="round" />
								<path
									d="M6.99984 4.08332C7.80525 4.08332 8.45817 3.43041 8.45817 2.62499C8.45817 1.81957 7.80525 1.16666 6.99984 1.16666C6.19442 1.16666 5.5415 1.81957 5.5415 2.62499C5.5415 3.43041 6.19442 4.08332 6.99984 4.08332Z"
									fill="url(#paint4_linear_76_5048)" stroke="url(#paint5_linear_76_5048)"
									stroke-linecap="round" stroke-linejoin="round" />
								<path
									d="M6.99984 12.8333C6.99984 11.2225 5.69399 9.91666 4.08317 9.91666C2.47234 9.91666 1.1665 11.2225 1.1665 12.8333"
									stroke="url(#paint6_linear_76_5048)" stroke-linecap="round"
									stroke-linejoin="round" />
								<path
									d="M12.8333 12.8333C12.8333 11.2225 11.5275 9.91666 9.91667 9.91666C8.30585 9.91666 7 11.2225 7 12.8333"
									stroke="url(#paint7_linear_76_5048)" stroke-linecap="round"
									stroke-linejoin="round" />
								<path
									d="M9.91683 7.00001C9.91683 5.38919 8.61098 4.08334 7.00016 4.08334C5.38935 4.08334 4.0835 5.38919 4.0835 7.00001"
									stroke="url(#paint8_linear_76_5048)" stroke-linecap="round"
									stroke-linejoin="round" />
								<defs>
									<linearGradient id="paint0_linear_76_5048" x1="3.5" y1="7.72917" x2="5.25"
										y2="10.3542" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint1_linear_76_5048" x1="3.5" y1="7.72917" x2="5.25"
										y2="10.3542" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint2_linear_76_5048" x1="9.3335" y1="7.72917" x2="11.0835"
										y2="10.3542" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint3_linear_76_5048" x1="9.3335" y1="7.72917" x2="11.0835"
										y2="10.3542" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint4_linear_76_5048" x1="6.4165" y1="1.89582" x2="8.1665"
										y2="4.52082" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint5_linear_76_5048" x1="6.4165" y1="1.89582" x2="8.1665"
										y2="4.52082" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint6_linear_76_5048" x1="2.9165" y1="10.6458" x2="4.054"
										y2="14.0583" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint7_linear_76_5048" x1="8.75" y1="10.6458" x2="9.8875"
										y2="14.0583" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint8_linear_76_5048" x1="5.8335" y1="4.81251" x2="6.971"
										y2="8.22501" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
								</defs>
							</svg>
						</text>
						<text class="orange-color">游客家属</text>
					</view>
				</view>
			</view>

			<!-- 底部 3 项核心数据统计 -->
			<view class="profile-stats-grid">
				<view class="p-stat-item">
					<text class="stat-num">5</text>
					<view class="stat-lbl-box">
						<text class="stat-icon"> <svg width="14" height="14" viewBox="0 0 14 14" fill="none"
								xmlns="http://www.w3.org/2000/svg">
								<path
									d="M11.958 1.45801C12.6024 1.45801 13.125 1.98067 13.125 2.625V11.667C13.1248 12.3112 12.6022 12.833 11.958 12.833H2.04199C1.39777 12.833 0.875176 12.3112 0.875 11.667V2.625C0.875 1.98067 1.39766 1.45801 2.04199 1.45801H11.958ZM2.04199 4.95801H11.958V2.625H2.04199V4.95801Z"
									fill="url(#paint0_linear_76_5056)" />
								<path d="M4.6665 1.16666V3.49999" stroke="url(#paint1_linear_76_5056)"
									stroke-linecap="round" stroke-linejoin="round" />
								<path d="M9.3335 1.16666V3.49999" stroke="url(#paint2_linear_76_5056)"
									stroke-linecap="round" stroke-linejoin="round" />
								<path d="M8.1665 9.91666H9.9165" stroke="#514435" stroke-linecap="round"
									stroke-linejoin="round" />
								<path d="M4.0835 9.91666H5.8335" stroke="#514435" stroke-linecap="round"
									stroke-linejoin="round" />
								<path d="M8.1665 7.58334H9.9165" stroke="#514435" stroke-linecap="round"
									stroke-linejoin="round" />
								<path d="M4.0835 7.58334H5.8335" stroke="#514435" stroke-linecap="round"
									stroke-linejoin="round" />
								<defs>
									<linearGradient id="paint0_linear_76_5056" x1="7" y1="1.45801" x2="7" y2="12.833"
										gradientUnits="userSpaceOnUse">
										<stop stop-color="#00C0E8" />
										<stop offset="1" stop-color="#2CE5A4" />
									</linearGradient>
									<linearGradient id="paint1_linear_76_5056" x1="5.1665" y1="1.16666" x2="5.1665"
										y2="3.49999" gradientUnits="userSpaceOnUse">
										<stop stop-color="#00C0E8" />
										<stop offset="1" stop-color="#2CE5A4" />
									</linearGradient>
									<linearGradient id="paint2_linear_76_5056" x1="9.8335" y1="1.16666" x2="9.8335"
										y2="3.49999" gradientUnits="userSpaceOnUse">
										<stop stop-color="#00C0E8" />
										<stop offset="1" stop-color="#2CE5A4" />
									</linearGradient>
								</defs>
							</svg>
						</text>
						<text class="stat-lbl">经验</text>
					</view>
				</view>
				<view class="p-stat-item">
					<text class="stat-num">142</text>
					<view class="stat-lbl-box">
						<text class="stat-icon"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"
								xmlns="http://www.w3.org/2000/svg">
								<path d="M3.2085 1.75V12.25" stroke="url(#paint0_linear_76_5061)" stroke-linecap="round"
									stroke-linejoin="round" />
								<path
									d="M3.2085 2.625H7.29183L9.3335 3.5H11.3752C11.6973 3.5 11.9585 3.76116 11.9585 4.08333V9.04167C11.9585 9.36384 11.6973 9.625 11.3752 9.625H9.3335L7.29183 8.75H3.2085V2.625Z"
									fill="url(#paint1_linear_76_5061)" stroke="url(#paint2_linear_76_5061)"
									stroke-linejoin="round" />
								<path d="M2.0415 12.25H4.37484" stroke="url(#paint3_linear_76_5061)"
									stroke-linecap="round" stroke-linejoin="round" />
								<defs>
									<linearGradient id="paint0_linear_76_5061" x1="3.5085" y1="4.375" x2="5.4195"
										y2="4.648" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint1_linear_76_5061" x1="5.8335" y1="4.375" x2="9.61204"
										y2="11.4598" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint2_linear_76_5061" x1="5.8335" y1="4.375" x2="9.61204"
										y2="11.4598" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
									<linearGradient id="paint3_linear_76_5061" x1="2.7415" y1="12.5" x2="3.0849"
										y2="13.7019" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FC7631" />
										<stop offset="1" stop-color="#DD502D" />
									</linearGradient>
								</defs>
							</svg>
						</text>
						<text class="stat-lbl">累计带团</text>
					</view>
				</view>
				<view class="p-stat-item">
					<text class="stat-num">98%</text>
					<view class="stat-lbl-box">
						<text class="stat-icon"><svg width="14" height="14" viewBox="0 0 14 14" fill="none"
								xmlns="http://www.w3.org/2000/svg">
								<path
									d="M4.37484 2.33334C2.60292 2.33334 1.1665 3.76977 1.1665 5.54168C1.1665 8.75001 4.95817 11.6667 6.99984 12.3452C9.0415 11.6667 12.8332 8.75001 12.8332 5.54168C12.8332 3.76977 11.3967 2.33334 9.62484 2.33334C8.53975 2.33334 7.58046 2.87202 6.99984 3.69654C6.41922 2.87202 5.45993 2.33334 4.37484 2.33334Z"
									fill="url(#paint0_linear_76_5066)" stroke="url(#paint1_linear_76_5066)"
									stroke-linecap="round" stroke-linejoin="round" />
								<defs>
									<linearGradient id="paint0_linear_76_5066" x1="6.99984" y1="2.33334" x2="9.16699"
										y2="12" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FF383C" />
										<stop offset="0.935801" stop-color="#FF5415" />
									</linearGradient>
									<linearGradient id="paint1_linear_76_5066" x1="6.99984" y1="2.33334" x2="6.99984"
										y2="12.3452" gradientUnits="userSpaceOnUse">
										<stop stop-color="#FF383C" />
										<stop offset="1" stop-color="#FF5415" />
									</linearGradient>
								</defs>
							</svg>
							️</text>
						<text class="stat-lbl">满意度</text>
					</view>
				</view>
			</view>
		</view>

		<!-- 3. 当前团队信息卡片 -->
		<view class="content-card card-shadow">
			<view class="card-header">
				<view class="header-icon-box">
					<image class="h-icon" src="/static/my/tag.png"></image>
				</view>
				<text class="card-title">当前团队信息</text>
			</view>

			<view class="info-list">
				<view class="info-row">
					<text class="row-label">团队名称</text>
					<text class="row-value bold-text">向海而生·情暖银龄-中国海洋文化二日游</text>
				</view>
				
				<view class="line"></view>
				
				<view class="info-row">
					<text class="row-label">目的地</text>
					<text class="row-value">浙江省/宁波市</text>
				</view>
				
				<view class="line"></view>
				
				<view class="info-row">
					<text class="row-label">行程日期</text>
					<text class="row-value">2026-07-04 至 2026-07-05</text>
				</view>
				
				<view class="line"></view>
				
				<view class="info-row">
					<text class="row-label">导游电话</text>
					<text class="row-value">13655848930</text>
				</view>
				
				<view class="line"></view>
				
				<view class="info-row">
					<text class="row-label">团队状态</text>
					<text class="row-value">结束</text>
				</view>
			</view>
		</view>

		<!-- 4. 今日工作汇总 -->
		<view class="content-card2">
			<view class="card-header">
				<view class="header-icon-box">
					<image class="h-icon" src="/static/my/tag2.png"></image>
				</view>
				<text class="card-title">今日工作汇总</text>
			</view>

			<view class="work-stats-grid">
				<view class="w-stat-box">
					<text class="w-num color-orange">30</text>
					<view class="w-lbl-row">
						<image class="w-icon" src="/static/my/w-icon1.png"></image>
						<text class="w-txt">健康监测</text>
					</view>
				</view>
				<view class="w-stat-box">
					<text class="w-num color-red">3</text>
					<view class="w-lbl-row">
						<image class="w-icon" src="/static/my/w-icon2.png"></image>
						<text class="w-txt">处理预警</text>
					</view>
				</view>
				<view class="w-stat-box">
					<text class="w-num color-dark">4</text>
					<view class="w-lbl-row">
						<image class="w-icon" src="/static/my/w-icon3.png"></image>
						<text class="w-txt">服务记录</text>
					</view>
				</view>
				<view class="w-stat-box">
					<text class="w-num color-green">2/8</text>
					<view class="w-lbl-row">
						<image class="w-icon" src="/static/my/w-icon4.png"></image>
						<text class="w-txt">已完成</text>
					</view>
				</view>
			</view>
		</view>

		<!-- 5. 快捷操作 -->
		<view class="content-card card-shadow">
			<view class="card-header">
				<view class="header-icon-box">
					<image class="h-icon" src="/static/my/tag3.png"></image>
				</view>
				<text class="card-title">快捷操作</text>
			</view>

			<view class="action-grid">
				<view class="action-tile">
					<image src="/static/my/tile-icon1.png" class="tile-icon"></image>
					<text class="tile-text">导出报告</text>
				</view>
				<view class="action-tile">
					<image src="/static/my/tile-icon2.png" class="tile-icon"></image>
					<text class="tile-text">群发通知</text>
				</view>
				<view class="action-tile">
					<image src="/static/my/tile-icon3.png" class="tile-icon"></image>
					<text class="tile-text">行程调整</text>
				</view>
				<view class="action-tile">
					<image src="/static/my/tile-icon4.png" class="tile-icon"></image>
					<text class="tile-text">批量上传</text>
				</view>
				<view class="action-tile">
					<image src="/static/my/tile-icon5.png" class="tile-icon"></image>
					<text class="tile-text">管理成员</text>
				</view>
				<view class="action-tile">
					<image src="/static/my/tile-icon6.png" class="tile-icon"></image>
					<text class="tile-text">系统设置</text>
				</view>
			</view>
		</view>

		<!-- 底部安全区域留白 -->
		<view class="safe-bottom-area"></view>
	</view>
</template>

<script setup>
	// UI 层面纯展示，不需要繁杂业务逻辑
</script>

<style lang="scss" scoped>
	/* ================== 色彩与设计变量 ================== */
	$page-bg: #F7F8FA;
	$text-title: #111111;
	$text-main: #1D2129;
	$text-sub: #86909C;

	$brand-orange: #FF6633;
	$brand-orange-grad: linear-gradient(135deg, #FF834E 0%, #FF5522 100%);
	$color-red: #F53F3F;
	$color-green: #00B42A;

	/* ================== 全局重置 ================== */
	.page-container {
		min-height: 100vh;
		background-color: $page-bg;
		font-family: -apple-system, BlinkMacSystemFont, "PingFang SC", "Helvetica Neue", Arial, sans-serif;
		position: relative;
		overflow-x: hidden;
		padding-bottom: 50rpx;
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
		height: 500rpx;
		background-image: url(/static/bg.png);
		background-size: 100% 100%;
		z-index: 0;
	}

	/* ================== 1. 顶部 Header ================== */
	.header-section {
		position: relative;
		z-index: 1;
		padding: 100rpx 32rpx 28rpx;
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

	/* ================== 2. 黑金个人卡片 ================== */
	.profile-card {
		position: relative;
		z-index: 1;
		margin: 10rpx 32rpx 32rpx;
		padding: 36rpx 32rpx 32rpx;
		border-radius: 32rpx;
		color: #FFFFFF;


		background: linear-gradient(12deg, #000000 0%, #7B5200 100%), #271500;

		.user-info-row {
			display: flex;
			align-items: center;
			margin-bottom: 32rpx;

			.avatar {
				width: 112rpx;
				height: 112rpx;
				border-radius: 20rpx;
				margin-right: 24rpx;
			}

			.user-detail {
				display: flex;
				flex-direction: column;

				.name-line {
					display: flex;
					align-items: center;

					margin-bottom: 24rpx;

					.user-name {
						font-family: PingFang SC, PingFang SC;
						font-weight: 500;
						font-size: 36rpx;
						color: #FFFFFF;

					}

					.role-pill {
						background: #695734;
						margin-left: 16rpx;
						width: 124rpx;
						height: 52rpx;
						font-size: 22rpx;
						color: #E5E5E5;
						border-radius: 32rpx;
						display: flex;
						align-items: center;
						justify-content: center;

						.arrow {
							margin-top: 10rpx;
							margin-left: 5rpx;
							font-size: 30rpx;
						}
					}
				}

				.user-sub {
					font-size: 24rpx;
					color: rgba(255, 255, 255, 0.6);
				}
			}
		}

		/* 角色切换区块 */
		.role-switch-panel {
			background: rgba(255, 255, 255, 0.08);
			border-radius: 32rpx;
			padding: 32rpx;
			margin-bottom: 28rpx;

			.switch-title {
				font-size: 22rpx;
				color: rgba(255, 255, 255, 0.6);
				display: block;
				margin-bottom: 16rpx;
			}

			.role-btn-group {
				display: flex;
				gap: 16rpx;
				margin-top: 16rpx;

				.role-btn {
					flex: 1;
					display: flex;
					align-items: center;
					justify-content: center;
					text-align: center;
					font-size: 24rpx;
					font-weight: 500;
					width: 162rpx;
					height: 56rpx;
					border-radius: 16rpx;

					.btn-icon {
						margin-top: 7rpx;
						margin-right: 8rpx;
					}

					&.active {
						border: 1rpx solid #FC7631;
						background: linear-gradient(146deg, #FC7631 0%, #DD502D 100%);
						font-family: PingFang SC, PingFang SC;
						font-weight: 400;
						color: #FFFFFF;
					}

					&.light {
						background: #FFFFFF;

						border: 1rpx solid #FC7631;
						font-family: PingFang SC, PingFang SC;
						font-weight: 400;
						color: #FC7631;
					}

					.orange-color {
						color: $brand-orange;
					}
				}
			}
		}

		/* 3项核心数据指标 */
		.profile-stats-grid {
			display: flex;
			justify-content: space-between;
			gap: 16rpx;

			.p-stat-item {

				width: 196rpx;
				height: 160rpx;
				background: rgba(255, 255, 255, 0.08);
				border-radius: 32rpx;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;

				.stat-num {
					margin-bottom: 8rpx;
					font-family: Roboto, Roboto;
					font-weight: 500;
					font-size: 56rpx;
					color: #FFFFFF;
				}

				.stat-lbl-box {
					display: flex;
					align-items: center;
					font-size: 22rpx;
					color: rgba(255, 255, 255, 0.7);

					.stat-icon {
						margin-top: 7rpx;
						margin-right: 6rpx;
						font-size: 20rpx;
					}

					.green-sq {
						width: 14rpx;
						height: 14rpx;
						background: $color-green;
						border-radius: 2rpx;
					}
				}
			}
		}
	}

	/* ================== 通用内容卡片 ================== */
	.content-card {
		position: relative;
		z-index: 1;
		background: #FFFFFF;
		border-radius: 32rpx;
		margin: 0 32rpx 32rpx;
		padding: 32rpx;

		.card-header {
			display: flex;
			align-items: center;
			margin-bottom: 28rpx;

			.header-icon-box {
				width: 44rpx;
				height: 44rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				margin-right: 12rpx;

				.h-icon {
					width: 32rpx;
					height: 32rpx;
				}
			}

			.card-title {
				font-size: 32rpx;
				font-weight: bold;
				color: $text-title;
			}
		}
	}
	
	.content-card2 {
		position: relative;
		z-index: 1;

		border-radius: 32rpx;
		margin: 0 32rpx 32rpx;
	
		.card-header {
			display: flex;
			align-items: center;
			margin-bottom: 28rpx;
	
			.header-icon-box {
				width: 44rpx;
				height: 44rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				margin-right: 12rpx;
	
				.h-icon {
					width: 32rpx;
					height: 32rpx;
				}
			}
	
			.card-title {
				font-size: 32rpx;
				font-weight: bold;
				color: $text-title;
			}
		}
	}
	

	/* ================== 3. 团队信息列表 ================== */
	.info-list {
		display: flex;
		flex-direction: column;
		gap: 24rpx;
		
		.line{
			// width: 311px;
			height: 2rpx;
			background-color: #E4E1DD;
		}

		.info-row {
			display: flex;
			justify-content: space-between;
			align-items: center;
			font-size: 28rpx;
			

			.row-label {
				width: 160rpx;
				
				font-family: PingFang SC, PingFang SC;
				font-weight: 400;
				font-size: 28rpx;
				color: #595959;
			}

			.row-value {
				text-align: right;
				font-family: PingFang SC, PingFang SC;
				font-weight: 500;
				font-size: 25rpx;
				color: #2A2A2A;

				&.bold-text {
					font-weight: bold;
					color: $text-title;
				}
			}
		}
	}

	/* ================== 4. 工作汇总网格 ================== */
	.work-stats-grid {
		display: flex;
		justify-content: space-between;
		gap: 16rpx;

		.w-stat-box {
			flex: 1;
			height: 200rpx;
			background: #FFFFFF;
			border-radius: 32rpx;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;

			.w-num {
				
				font-family: Roboto, Roboto;
				font-weight: 500;
				font-size: 56rpx;
				color: #FC7631;
				margin-bottom: 10rpx;
			}
			
			.w-txt{
				font-family: PingFang SC, PingFang SC;
				font-weight: 500;
				font-size: 24rpx;
				color: #2A2A2A;
			}

			.color-orange {
				color: $brand-orange;
			}

			.color-red {
				color: $color-red;
			}

			.color-dark {
				color: $text-title;
			}

			.color-green {
				color: $color-green;
			}

			.w-lbl-row {
				display: flex;
				align-items: center;
				font-size: 22rpx;
				color: $text-sub;

				.w-icon {
					width: 32rpx;
					height: 32rpx;
					margin-right: 4rpx;
				}
			}
		}
	}

	/* ================== 5. 快捷操作 3x2 网格 ================== */
	.action-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 20rpx;

		.action-tile {
			background: #F8F9FA;
			border-radius: 20rpx;
			height: 140rpx;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;

			.tile-icon {
				width: 30rpx;
				height: 30rpx;
				margin-bottom: 12rpx;
			}

			.tile-text {
				font-size: 26rpx;
				color: $text-main;
				font-weight: 500;
			}
		}
	}

	.safe-bottom-area {
		height: 60rpx;
	}
</style>