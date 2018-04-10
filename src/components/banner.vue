<template>
	<div class="banner">
		<swiper class="swiper" :options="swiperOption" ref="mySwiper">
			<swiper-slide v-for='(item,index) in json' :key='index'>
                <router-link :to="`/detail/${item.sound.id}`">
                    <img :src="item.sound.pic_640">
                </router-link>
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
		</swiper>
	</div>
</template>

<script>
export default{
	props:{
		json: Array
	},
	data() {
		return {
			swiperOption: {
				notNextTick: true,
				pagination: {
					el: '.swiper-pagination'
				},
				paginationClickable: true,
				autoplay: true,
	          	loop:true,
    			autoplayDisableOnInteraction : false,    //注意此参数，默认为true
			}
		}
	}
}
</script>

<style lang="stylus">
banner_height = toRem(160)
.banner
	width 100%
	padding 10px
	height banner-height
	background-color #e8e8e8
	.swiper
		width 100%
		height 100%
		.swiper-slide
			img
				width 100%
				height auto
		.swiper-pagination-bullet
			background #fff
</style>