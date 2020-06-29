# react-unit
react框架的后台系统模板

# src目录使用@代替

webpack.config.js文件配置alias：'@': path.resolve(__dirname,'../src'),

# 配置使用less

安装依赖：yarn add less less-loader --save

webpack.config.js文件添加less正则：

const lessRegex = /\.less$/;
const lessModuleRegex = /\.module\.less$/;

修改 getStyleLoaders 函数，添加代码：

getStyleLoaders = (cssOptions, lessOptions, preProcessor)

{
    loader: require.resolve('less-loader'),
    options: lessOptions,
}

模仿代码中提供的sassRegex代码，添加如下代码：

{
    test: lessRegex,
    exclude: cssModuleRegex,
    use: getStyleLoaders({
         importLoaders: 1,
         sourceMap: isEnvProduction && shouldUseSourceMap,
    }),
    sideEffects: true,
},
{
    test: lessModuleRegex,
    use: getStyleLoaders({
         importLoaders: 1,
         sourceMap: isEnvProduction && shouldUseSourceMap,
         modules: true,
         getLocalIdent: getCSSModuleLocalIdent,
    }),
},
