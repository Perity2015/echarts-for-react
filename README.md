# echarts-for-react

A very simple echarts(v3.0) wrapper for react.

[![Build Status](https://travis-ci.org/hustcc/echarts-for-react.svg?branch=master)](https://travis-ci.org/hustcc/echarts-for-react) [![npm](https://img.shields.io/npm/v/echarts-for-react.svg?style=flat-square)](https://www.npmjs.com/package/echarts-for-react) [![npm](https://img.shields.io/npm/dt/echarts-for-react.svg?style=flat-square)](https://www.npmjs.com/package/echarts-for-react) [![npm](https://img.shields.io/npm/l/echarts-for-react.svg?style=flat-square)](https://www.npmjs.com/package/echarts-for-react)

# 1. install

```sh
npm install echarts-for-react
```

How to run the demo:

```sh
git clone git@github.com:hustcc/echarts-for-react.git

npm install

npm start
```

then open [http://127.0.0.1:8080/](http://127.0.0.1:8080/) in your browser. or see [http://git.hust.cc/echarts-for-react/](http://git.hust.cc/echarts-for-react/)


# 2. usage

Simple demo code. for more example can see: [http://git.hust.cc/echarts-for-react/](http://git.hust.cc/echarts-for-react/)

```js
import React from 'react';
import ReactEcharts from 'echarts-for-react';  // or var ReactEcharts = require('echarts-for-react');

<ReactEcharts
    option={this.getOption()} 
	notMerge={true}
	lazyUpdate={true}
	theme={"theme_name"}
	onChartReady={this.onChartReadyCallback}
    onEvents={EventsDict} />
```


# 3. component props

 - **`option`** (required, object)

the echarts option config, can see [http://echarts.baidu.com/option.html#title](http://echarts.baidu.com/option.html#title).

 - **`notMerge`** (required, object)

when `setOption`, not merge the data, default is `false`. See [http://echarts.baidu.com/api.html#echartsInstance.setOption](http://echarts.baidu.com/api.html#echartsInstance.setOption).

 - **`lazyUpdate`** (required, object)

when `setOption`, lazy update the data, default is `false`. See [http://echarts.baidu.com/api.html#echartsInstance.setOption](http://echarts.baidu.com/api.html#echartsInstance.setOption).

 - **`style`** (optional, object)

the `style` of echarts div. `object`, default is {height: '300px'}.

 - **`className`** (optional, string)

the `class` of echarts div. you can setting the css style of charts by class name.

 - **`theme`** (optional, string)

the `theme` of echarts. `string`, should `registerTheme` before use it (theme object format: [https://github.com/ecomfe/echarts/blob/master/theme/dark.js](https://github.com/ecomfe/echarts/blob/master/theme/dark.js)). e.g.


```js
// import echarts
import echarts from 'echarts'; 
...
// register theme object
echarts.registerTheme('my_theme', {
  backgroundColor: '#f4cccc'
});
...
// render the echarts use option `theme`
<ReactEcharts 
    option={this.getOption()} 
    style={{height: '300px', width: '100%'}} 
	className='echarts-for-echarts' 
    theme='my_theme' /> 

```

 - **`onChartReady`** (optional, function)

when the chart is ready, will callback the function with the `echarts object` as it's paramter.

 - **`loadingOption`** (optional, object)

the echarts loading option config, can see [http://echarts.baidu.com/api.html#echartsInstance.showLoading](http://echarts.baidu.com/api.html#echartsInstance.showLoading).

 - **`showLoading`** (optional, bool, default: false)

`bool`, when the chart is rendering, show the loading mask.

 - **`onEvents`** (optional, array(string=>function) )

binding the echarts event, will callback with the `echarts event object`, and `the echart object` as it's paramters. e.g: 

```js
let onEvents = {
    'click': this.onChartClick,
    'legendselectchanged': this.onChartLegendselectchanged
}
...
<ReactEcharts
    option={this.getOption()} 
    style={{height: '300px', width: '100%'}} 
    onEvents={onEvents} />
```
for more event key name, see: [http://echarts.baidu.com/api.html#events](http://echarts.baidu.com/api.html#events)


# 4. Component API & Echarts API

the Component only has `one API` named `getEchartsInstance`.

 - **`getEchartsInstance()`** : get the echarts instance object, then you can use any `API of echarts`.

for example:

```js
// render the echarts component below with rel
<ReactEcharts ref='echarts_react'
    option={this.getOption()} />

// then get the `ReactEcharts` use this.refs.echarts_react

let echarts_instance = this.refs.echarts_react.getEchartsInstance();
// then you can use any API of echarts.
let base64 = echarts_instance.getDataURL();
```

**About API of echarts, can see** [http://echarts.baidu.com/api.html#echartsInstance](http://echarts.baidu.com/api.html#echartsInstance).

you can use the API to do:

1. `binding / unbinding` event.
2. `dynamic charts` with dynamic data.
3. get the echarts dom / dataURL / base64, save the chart to png.
4. `release` the charts.


# 5. LICENSE

MIT
