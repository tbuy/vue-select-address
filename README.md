# 地址选择组件

> 基于vue的简单地址（省/市/区）选择

[demo](http://jssdk.sinaapp.com/widget/share.php)

## 安装

```
npm install
```

## 运行

```
npm run dev
```

## api

名称 | 类型 | 默认值 | 是否必选 | 描述
---|--- |--- |--- | ---
provinceList | Array | [] | no | 省级区域列表 例如:[{code: 1, area: '辽宁'}，{code: 2, area: '北京'}]
cityList | Array | [] | no | 市级区域列表 例如:[{code: 1, area: '辽宁'}，{code: 2, area: '北京'}]
districtList | Array | [] | no | 区级区域列表 例如:[{code: 1, area: '辽宁'}，{code: 2, area: '北京'}]
province | Object 或 String | 无 | yes | 选中的省级名称 例如:{code: 1, area: '辽宁'} 或者 默认显示的文案 例如:'请选择'
city | Object 或 String | 无 | yes | 选中的市级名称 例如:{code: 1, area: '辽宁'} 或者 默认显示的文案 例如:'请选择'
district | Object 或 String | 无 | yes | 选中的区级名称 例如:{code: 1, area: '辽宁'} 或者 默认显示的文案 例如:'请选择'
