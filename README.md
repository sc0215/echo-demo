# my-music-master

> A Vue.js music project        
demo：https://bugsc.github.io/githueEchoOnlineSeek/#/index
# 主要用到的插件
 "amfe-flexible": "^2.2.1",     
 "axios": "^0.17.1",     
 "babel-polyfill": "^6.26.0",    
 "jquery": "^3.3.1",     
 "material-design-icons": "^3.0.1",     
 "mockjs": "^1.0.1-beta3",     
 "muse-ui": "^2.1.0",     
 "qs": "^6.5.1",     
 "stylus": "^0.54.5",
 "stylus-loader": "^3.0.2",     
 "vue": "^2.5.13",     
 "vue-awesome-swiper": "^3.1.3",     
 "vue-progressbar": "^0.7.4",     
 "vue-router": "^3.0.1",     
 "vue-style-loader": "^3.1.2",     
 "vuex": "^3.0.1"
	
# 怎么应用公共.styl文件以及怎么在vue中使用jQuery
	1、.styl文件的引用，
		①、先找到build文件夹
		②、然后再找到build文件夹下，utils.js文件
		③、在util.js文件第59行添加：var cssDir = path.resolve(__dirname, '../src/assets/css')（css目录路径）
		④、在.js文件66行return数据stylus修改为：generateLoaders('stylus', { import: [cssDir+'/*.styl'] })
	2、jQuery插件的引用
		①、先找到build文件夹
		②、然后再找到build文件夹下，webpack.dev.conf.js文件和webpack.prod.conf.js文件
		③、分别在webpack.dev.conf.js文件第59行，webpack.prod.conf.js文件第122行添加
		new webpack.ProvidePlugin({      
			$: 'jquery',       
			jQuery: 'jquery',      
			'window.jQuery': 'jquery',      
			'window.$': 'jquery',     
		})
# vue-router在这里开启了history如下
		export default new Router({
				// mode: 'history', // 后端支持可开
				https://router.vuejs.org/zh-cn/advanced/scroll-behavior.html
				scrollBehavior(to, from, savedPosition) {
					if( savedPosition ) {
									// 使用场景：数据是请求的，并且不使用keep-alive。
									// to.meta.position = savedPosition
						return savedPosition
					} else {
						return { x: 0, y: 0 }
					}
				},
				routes: [
					{
						path: '/index',
						component: index
					},
					{
						path: '/detail/:id',
						component: detail
					},
						// 注意：开启history模式，后端就无法返回404页面了，
						// 所以前端需要对所有情况做一个统一处理，这里可以写一个404页面或者像我一样返回主页
						// 优先级放在最下面
						{
								path: '*',
								redirect: '/index'
						}
				]
			})
# 打包在线显示
	1、项目资源无法加载解决方法：
		①、打开项目根目录　config　下的　index.js　文件，进行如下修改：
			☞将　assetsPublicPath: ‘/‘,　改为　assetsPublicPath: ‘./‘。
	2、字体图标无法加载解决方法：
		①、打开根目录下　build　中的　utils.js　文件，找到
			 // Extract CSS when that option is specified
			 // (which is the case during production build)
			进行如下修改：
			☞控制build样式文件代码中添加　publicPath: ‘../../‘
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
