# react 的配置插件react-app-rewired介绍。
  1. 安装后启动命令换成react-app-rewired react等
  2. 所有的配置都config-overrides.js已插入的形式。
  
    module.exports = function override(config, env) { 
    // 已插入的形式。如数组的unshift,注意不能用push webpack的加载顺序是从后向前加载。
      return config
    }


## 1.css的module的配置。注意rules的加载顺序从后向前加载处理
  react为例配置less，采用插件react-app-rewired。less-loads->(postcss-loader->)css-loader->style-loader

        const getStyleLoaders = (cssOptions, preProcessor) => {
        const loaders = [
            require.resolve('style-loader'),
            {
                loader: require.resolve('css-loader'),
                options: cssOptions,
            },
            {
                loader: require.resolve('postcss-loader'),
                options: {
                    ident: 'postcss',
                    plugins: () => [
                        require('postcss-flexbugs-fixes'),
                        require('postcss-preset-env')({
                            autoprefixer: {
                                flexbox: 'no-2009',
                            },
                            stage: 3,
                        }),
                        postcssNormalize(),
                    ],
                    sourceMap: true,
                },
            },
        ].filter(Boolean);
        if (preProcessor) {
            loaders.push(
                {
                    loader: require.resolve('resolve-url-loader'),
                    options: {
                        sourceMap: true,
                    },
                },
                {
                    loader: require.resolve(preProcessor),
                    options: {
                        sourceMap: true,
                    },
                }
            );
        }
        return loaders;
    }
    
 ### 1. css全局文件文件加载  
 
    module.rules[2].oneOf.unshift({
        test: /\.global\.less$/,
        use: getStyleLoaders({importLoaders: 1,sourceMap: true}, 'less-loader'),
        sideEffects: true,
    })
    
 ### 2. css全局文件文件加载，过滤掉global.less全局样式文件,modules: true为模块化，加hash。
  
    module.rules[2].oneOf.unshift({
        test: /\.less$/,
        exclude: /\.global\.less$/,
        use: getStyleLoaders({importLoaders: 1,sourceMap: true, modules: true}, 'less-loader'),
        sideEffects: true,
    })
    
 ### 3. 直接将所有的css样式封装到js文件中，以<style></style>方式加载。这样让css单独文件提取的插件无效。MiniCssExtractPlugin插件。
 
    module.rules[2].oneOf.unshift({
        test: /\.css$/,
        exclude: /node_modules\.css/,
        use:getStyleLoaders({importLoaders: 2, localIdentName: '[name]__[local]--[hash:base64:5]'}),
        sideEffects: true,
    })

### 4. config.resolve.symlinks 配置项将link的包解析到它们的符号链接位置，在自己开发包本地link时需要配置这个参数值为false，不然会造成包无法引入；
参考链接 https://www.jianshu.com/p/ca252cd667df
