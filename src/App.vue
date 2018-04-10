<template>
	<div id="app"  :class="{'musicBar-on': audio.data}">
		<!-- 视图层 -->
		<keep-alive>
			<router-view></router-view>
		</keep-alive>
		<!-- 音乐控制条 -->
		<music-bar></music-bar>
		<!-- 页面加载进度条 -->
		<vue-progress-bar></vue-progress-bar>
	</div>
</template>

<script>
import { mapState, mapMutations } from 'vuex'
export default {
	computed: {
		...mapState([
			'audio'
		])
	},
	methods: {
		...mapMutations([
			'set_app_cache'
		])
	},
	created() {
		this.set_app_cache()
		this.$Progress.start()
		this.$router.beforeEach((to, from, next) => {
			this.$Progress.start()
			next()
		})
		this.$router.afterEach((to, from) => {
			this.$Progress.finish()
		})
	},
	mounted() {
		// 加载进度条，结束
		this.$Progress.finish()
	}

}
</script>

<style lang="stylus">
	#app 
		position relative 
		min-height inherit 
		background #eee 
		&.musicBar-on 
			padding-bottom 1.3rem
</style>