<template>
	<div class="user-wrapper">
		<div class="content-box">
			<a href="https://pro.loacg.com/docs/getting-started" target="_blank">
				<span class="action">
					<a-icon type="question-circle-o"></a-icon>
				</span>
			</a>
			<notice-icon class="action" />
			<a-dropdown>
				<span class="action ant-dropdown-link user-dropdown-menu">
					<a-avatar class="avatar" size="small" :src="avatar" />
					<span>{{ nickname }}</span>
				</span>
				<a-menu slot="overlay" class="user-dropdown-menu-wrapper">
					<a-menu-item key="0">
						<router-link :to="{ name: 'center' }">
							<a-icon type="user" />
							<span>个人中心</span>
						</router-link>
					</a-menu-item>
					<a-menu-item key="1">
						<router-link :to="{ name: 'settings' }">
							<a-icon type="setting" />
							<span>账户设置</span>
						</router-link>
					</a-menu-item>
					<a-menu-item key="2" disabled>
						<a-icon type="setting" />
						<span>测试</span>
					</a-menu-item>
					<a-menu-divider />
					<a-menu-item key="3">
						<a href="javascript:;" @click="handleLogout">
							<a-icon type="logout" />
							<span>退出登录</span>
						</a>
					</a-menu-item>
				</a-menu>
			</a-dropdown>
		</div>
	</div>
</template>

<script>
	import NoticeIcon from '@/components/NoticeIcon'
	import {mapActions,mapGetters} from 'vuex'
	export default {
		name: 'UserMenu',
		components: {
			NoticeIcon
		},
		computed: {
			...mapGetters(['nickname', 'avatar'])

		},
		methods: {
			handleLogout() {
				this.$confirm({
					title: '提示',
					content: '真的要注销登录吗 ?',
					onOk: () => {
						return this.$store.dispatch('logout').then(() => {
							this.$router.push({
								path: '/user/login'
							})
							/* setTimeout(() => {
								window.location.reload()
							}, 16) */
						}).catch(err => {
							this.$message.error({
								title: '错误',
								description: err.message
							})
						})
					},
					onCancel() {}
				})
			},
		}
	}
</script>

<style lang="less" scoped>
	.trigger {
		font-size: 18px;
		line-height: 64px;
		padding: 0 24px;
		cursor: pointer;
		transition: color 0.3s;

		&:hover {
			color: #1890ff;
		}
	}

	.handle-signout {
		// cursor: pointer;
		color: #606266;

		&:hover {
			// text-decoration: underline;
			color: #4cd480;
		}
	}

	.crumbs {
		display: flex;

		.curmb-content {
			flex: 1;
			display: flex;
			justify-content: space-between;
		}

		.lang-select-avator {
			margin-top: -4px;
			align-items: center;
			margin-right: 24px;
			display: flex;

			.select-language-box {
				margin-top: 5px;
			}
		}
	}

	/deep/ .ant-breadcrumb {
		line-height: 64px;
		height: 64px;
	}
</style>
