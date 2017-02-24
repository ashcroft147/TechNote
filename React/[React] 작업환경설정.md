## Dependency 및 Plugin 설치하기

React 사용을 위한 의존 Package들을 설치한다.
~~~
$ npm install react react-dom --save --legacy-bundling
~~~

React를 Transpile 하기위해서는 babel을 사용한다.

1) 필요한 Module
    "babel-core": "^6.22.1",
    "babel-loader": "^6.2.10",
    "babel-preset-es2015": "^6.22.0",
    "babel-preset-react": "^6.22.0",

webpack.config.js에 babel transpile을 위한 loader를 설정해 주어야 한다. 

1) 
        { 
            test: /\.jsx?$/,         // Match both .js and .jsx files
            exclude: /node_modules/, 
            loader: "babel",
            query:
            {
                presets:['es2015','react']
            }
        },
