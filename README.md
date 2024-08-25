~1.2.3 :=
>=1.2.3 <1.(2+1).0 :=
>=1.2.3 <1.3.0-0

^1.2.3 :=
>=1.2.3 <2.0.0-0

typescript 5.5.4 can't be used in webstorm,so i use 4.9.5.

Enabling esModuleInterop will also enable allowSyntheticDefaultImports.

Conclusion 

提升开发体验:
1. devtool
2. 加快构建速度 
- hmr
- cache for babel and eslint

提升用户体验：
1. 减小代码体积
- tree-shaking 
- babel(@babel/plugin-transform-runtime)
- minimizer
2. code-split
3. browser-cache + contentHash

other
减小体积
```Javascript
// webpack.config.js
const config = {
    module: {
        rules: [{
            test: /\.jsx?$/,
            loader: "babel-loader",
            options: {
                cacheDirectory: true,
                plugins: ["@babel/plugin-transform-runtime"], // 减少代码体积
            }
        }]
    },
    optimization: {
        runtimeChunk: {
            name: (entrypoint) => `runtime~${entrypoint.name}.js`
        }
    }
}
```

兼容代码
```Javascript
// index.js
import "core-js";

// babel.config.js
module.exports= {
    preset: [
        '@babel/preset-env',
        {useBuiltIns: 'usage', corejs: {version: '3', proposals: true}}
    ]
}
```

