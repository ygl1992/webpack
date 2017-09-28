# 安装webpack
1.npm init

2.npm install --save-dev webpack 或者 cnpm install --save-dev webpack 

# 新建webpack.config.js文件并配置
	const path = require('path');
	const webpack = require('webpack');
	
	module.exports={
	    //入口文件的配置项
	    entry:{
			//里面的entery是可以随便写的
    		entry:'./src/entry.js'
		},
	    //出口文件的配置项
	    output:{
			//打包的路径文件夹
		    path:path.resolve(__dirname,'dist'),
		    //打包的文件名称
			//[name] entry.js
			//[hash] 7a6e1c7c73b53fa83c50.js
		    filename:'bundle.js'
		},
	    //模块：例如解读CSS,图片如何转换，压缩
	    module:{
			loaders: [
				{test: /\.css$/, loader: 'style-loader!css-loader'},
				//图片大小（bytes）小于limit就以Data URL的形式引入图片，大于就用图片地址引用。
				{test: /\.(png|jpg)$/, loader: 'url-loader?limit=10240'}
			]
		},
	    //插件，用于生产模版和各项功能
	    plugins:[
			new webpack.optimize.UglifyJsPlugin({
				compress: {
					warnings: false
				}
			})
		],
	    //配置webpack开发服务功能
	    devServer:{
			contentBase: './',		  //本地服务器所加载的页面所在的目录
	        host: '192.168.1.158', 	  //本地IP地址
	        historyApiFallback: true, //不跳转
	        inline: true, 			  //实时刷新
	        port: '3333' 			  //端口号
		}
	}