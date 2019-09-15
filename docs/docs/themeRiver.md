---
id: themeRiver
title: ThemeRiver
sidebar_label: ThemeRiver（主题河流图）
---

> 是一种特殊的流图, 它主要用来表示事件或主题等在一段时间内的变化。

## API
```go
// 实例化图表
func NewThemeRiver(routers ...RouterOpts) *ThemeRiver
// 新增数据及配置项
func Add(name string, data interface{}, options ...seriesOptser) *ThemeRiver
// 新增 JS 函数
func AddJSFuncs(fn ...string)
// 设置全局配置项
func SetGlobalOptions(options ...globalOptser)
// 设置全部 Series 配置项
func SetSeriesOptions(options ...seriesOptser)
// 负责渲染图表，支持传入多个实现了 io.Writer 接口的对象
func Render(w ...io.Writer) error
```

## 预定义
> Note: 示例用到的一些变量及方法，部分重复的以后代码中不会再次列出
```go
var trRawData = [][]int{
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 49, 67, 16, 0, 19, 19, 0, 0, 1, 10, 5, 6, 1, 1, 0, 25, 0, 0, 0},
    {0, 6, 3, 34, 0, 16, 1, 0, 0, 1, 6, 0, 1, 56, 0, 2, 0, 2, 0, 0},
    {0, 8, 13, 15, 0, 12, 23, 0, 0, 1, 0, 1, 0, 0, 6, 0, 0, 1, 0, 1},
    {0, 9, 28, 0, 91, 6, 1, 0, 0, 0, 7, 18, 0, 9, 16, 0, 1, 0, 0, 0},
    {0, 3, 42, 36, 21, 0, 1, 0, 0, 0, 0, 16, 30, 1, 4, 62, 55, 1, 0, 0},
    {0, 7, 13, 12, 64, 5, 0, 0, 0, 8, 17, 3, 72, 1, 1, 53, 1, 0, 0, 0},
    {1, 14, 13, 7, 8, 8, 7, 0, 1, 1, 14, 6, 44, 8, 7, 17, 21, 1, 0, 0},
    {0, 6, 14, 2, 14, 1, 0, 0, 0, 0, 2, 2, 7, 15, 6, 3, 0, 0, 0, 0},
    {0, 9, 11, 3, 0, 8, 0, 0, 14, 2, 0, 1, 1, 1, 7, 13, 2, 1, 0, 0},
    {0, 7, 5, 10, 8, 21, 0, 0, 130, 1, 2, 18, 6, 1, 5, 1, 4, 1, 0, 7},
    {0, 2, 15, 1, 5, 5, 0, 0, 6, 0, 0, 0, 4, 1, 3, 1, 17, 0, 0, 9},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {6, 27, 26, 1, 0, 11, 1, 0, 0, 0, 1, 1, 2, 0, 0, 9, 1, 0, 0, 0},
    {31, 81, 11, 6, 11, 0, 0, 0, 0, 0, 0, 0, 3, 2, 0, 3, 14, 0, 0, 12},
    {19, 53, 6, 20, 0, 4, 37, 0, 30, 86, 43, 7, 5, 7, 17, 19, 2, 0, 0, 5},
    {0, 22, 14, 6, 10, 24, 18, 0, 13, 21, 5, 2, 13, 35, 7, 1, 8, 0, 0, 1},
    {0, 56, 5, 0, 0, 0, 0, 0, 7, 24, 0, 17, 7, 0, 0, 3, 0, 0, 0, 8},
    {18, 29, 3, 6, 11, 0, 15, 0, 12, 42, 37, 0, 3, 3, 13, 8, 0, 0, 0, 1},
    {32, 39, 37, 3, 33, 21, 6, 0, 4, 17, 0, 11, 8, 2, 3, 0, 23, 0, 0, 17},
}

var trLabels = []string{
    "The Sea and Cake",
    "Andrew Bird",
    "Laura Veirs",
    "Brian Eno",
    "Christopher Willits",
    "Wilco",
    "Edgar Meyer",
    "B\xc3\xa9la Fleck",
    "Fleet Foxes",
    "Kings of Convenience",
    "Brett Dennen",
    "Psapp",
    "The Bad Plus",
    "Feist",
    "Battles",
    "Avishai Cohen",
    "Rachael Yamagata",
    "Norah Jones",
    "B\xc3\xa9la Fleck and the Flecktones",
    "Joshua Redman",
}

var trTime = [][]interface{}{
    {"2015/11/08", 10, "DQ"}, {"2015/11/09", 15, "DQ"}, {"2015/11/10", 35, "DQ"},
    {"2015/11/11", 38, "DQ"}, {"2015/11/12", 22, "DQ"}, {"2015/11/13", 16, "DQ"},
    {"2015/11/14", 7, "DQ"}, {"2015/11/15", 2, "DQ"}, {"2015/11/16", 17, "DQ"},
    {"2015/11/17", 33, "DQ"}, {"2015/11/18", 40, "DQ"}, {"2015/11/19", 32, "DQ"},
    {"2015/11/20", 26, "DQ"}, {"2015/11/21", 35, "DQ"}, {"2015/11/22", 40, "DQ"},
    {"2015/11/23", 32, "DQ"}, {"2015/11/24", 26, "DQ"}, {"2015/11/25", 22, "DQ"},
    {"2015/11/26", 16, "DQ"}, {"2015/11/27", 22, "DQ"}, {"2015/11/28", 10, "DQ"},
    {"2015/11/08", 35, "TY"}, {"2015/11/09", 36, "TY"}, {"2015/11/10", 37, "TY"},
    {"2015/11/11", 22, "TY"}, {"2015/11/12", 24, "TY"}, {"2015/11/13", 26, "TY"},
    {"2015/11/14", 34, "TY"}, {"2015/11/15", 21, "TY"}, {"2015/11/16", 18, "TY"},
    {"2015/11/17", 45, "TY"}, {"2015/11/18", 32, "TY"}, {"2015/11/19", 35, "TY"},
    {"2015/11/20", 30, "TY"}, {"2015/11/21", 28, "TY"}, {"2015/11/22", 27, "TY"},
    {"2015/11/23", 26, "TY"}, {"2015/11/24", 15, "TY"}, {"2015/11/25", 30, "TY"},
    {"2015/11/26", 35, "TY"}, {"2015/11/27", 42, "TY"}, {"2015/11/28", 42, "TY"},
    {"2015/11/08", 21, "SS"}, {"2015/11/09", 25, "SS"}, {"2015/11/10", 27, "SS"},
    {"2015/11/11", 23, "SS"}, {"2015/11/12", 24, "SS"}, {"2015/11/13", 21, "SS"},
    {"2015/11/14", 35, "SS"}, {"2015/11/15", 39, "SS"}, {"2015/11/16", 40, "SS"},
    {"2015/11/17", 36, "SS"}, {"2015/11/18", 33, "SS"}, {"2015/11/19", 43, "SS"},
    {"2015/11/20", 40, "SS"}, {"2015/11/21", 34, "SS"}, {"2015/11/22", 28, "SS"},
    {"2015/11/23", 26, "SS"}, {"2015/11/24", 37, "SS"}, {"2015/11/25", 41, "SS"},
    {"2015/11/26", 46, "SS"}, {"2015/11/27", 47, "SS"}, {"2015/11/28", 41, "SS"},
    {"2015/11/08", 10, "QG"}, {"2015/11/09", 15, "QG"}, {"2015/11/10", 35, "QG"},
    {"2015/11/11", 38, "QG"}, {"2015/11/12", 22, "QG"}, {"2015/11/13", 16, "QG"},
    {"2015/11/14", 7, "QG"}, {"2015/11/15", 2, "QG"}, {"2015/11/16", 17, "QG"},
    {"2015/11/17", 33, "QG"}, {"2015/11/18", 40, "QG"}, {"2015/11/19", 32, "QG"},
    {"2015/11/20", 26, "QG"}, {"2015/11/21", 35, "QG"}, {"2015/11/22", 40, "QG"},
    {"2015/11/23", 32, "QG"}, {"2015/11/24", 26, "QG"}, {"2015/11/25", 22, "QG"},
    {"2015/11/26", 16, "QG"}, {"2015/11/27", 22, "QG"}, {"2015/11/28", 10, "QG"},
    {"2015/11/08", 10, "SY"}, {"2015/11/09", 15, "SY"}, {"2015/11/10", 35, "SY"},
    {"2015/11/11", 38, "SY"}, {"2015/11/12", 22, "SY"}, {"2015/11/13", 16, "SY"},
    {"2015/11/14", 7, "SY"}, {"2015/11/15", 2, "SY"}, {"2015/11/16", 17, "SY"},
    {"2015/11/17", 33, "SY"}, {"2015/11/18", 40, "SY"}, {"2015/11/19", 32, "SY"},
    {"2015/11/20", 26, "SY"}, {"2015/11/21", 35, "SY"}, {"2015/11/22", 4, "SY"},
    {"2015/11/23", 32, "SY"}, {"2015/11/24", 26, "SY"}, {"2015/11/25", 22, "SY"},
    {"2015/11/26", 16, "SY"}, {"2015/11/27", 22, "SY"}, {"2015/11/28", 10, "SY"},
    {"2015/11/08", 10, "DD"}, {"2015/11/09", 15, "DD"}, {"2015/11/10", 35, "DD"},
    {"2015/11/11", 38, "DD"}, {"2015/11/12", 22, "DD"}, {"2015/11/13", 16, "DD"},
    {"2015/11/14", 7, "DD"}, {"2015/11/15", 2, "DD"}, {"2015/11/16", 17, "DD"},
    {"2015/11/17", 33, "DD"}, {"2015/11/18", 4, "DD"}, {"2015/11/19", 32, "DD"},
    {"2015/11/20", 26, "DD"}, {"2015/11/21", 35, "DD"}, {"2015/11/22", 40, "DD"},
    {"2015/11/23", 32, "DD"}, {"2015/11/24", 26, "DD"}, {"2015/11/25", 22, "DD"},
    {"2015/11/26", 16, "DD"}, {"2015/11/27", 22, "DD"}, {"2015/11/28", 10, "DD"},
}
```

## Demo

平行坐标系需要配置 `ThemeRiver Options`，配置项详细参数可参考 [全局配置项#ThemeRiver Options](/docs/global_options#themeriver-options)

### ThemeRiver-示例图
```go
tr := charts.NewThemeRiver()
tr.SetGlobalOptions(
    charts.TitleOpts{Title: "ThemeRiver-示例图"},
    // 如果需要隐藏 Legend 则把 Data 设置为 []string{}
    charts.LegendOpts{Data: []string{}},
)
data := make([][]interface{}, 0)
for i := 0; i < len(trRawData); i++ {
    for j := 0; j < len(trRawData[i]); j++ {
        data = append(data, []interface{}{j, trRawData[i][j], trLabels[i]})
    }
}
tr.Add("themeRiver", data)
```
![](https://user-images.githubusercontent.com/19553554/52798264-8c706980-30b2-11e9-8666-9fdd63588130.png)


### ThemeRiver-SingleAxis(最大值)
```go
tr := charts.NewThemeRiver()
tr.SetGlobalOptions(
    charts.TitleOpts{Title: "ThemeRiver-SingleAxis(最大值)"},
    // 如果需要隐藏 Legend 则把 Data 设置为 []string{}
    charts.LegendOpts{Data: []string{}},
    charts.SingleAxisOpts{Max: "dataMax"},
)
data := make([][]interface{}, 0)
for i := 0; i < len(trRawData); i++ {
    for j := 0; j < len(trRawData[i]); j++ {
        data = append(data, []interface{}{j, trRawData[i][j], trLabels[i]})
    }
}
tr.Add("themeRiver", data)
```
![](https://user-images.githubusercontent.com/19553554/52798273-909c8700-30b2-11e9-8a69-e54a4546de2b.png)


### ThemeRiver-SingleAxis(时间轴)
```go
tr := charts.NewThemeRiver()
tr.SetGlobalOptions(
    charts.TitleOpts{Title: "ThemeRiver-SingleAxis(时间轴)"},
    charts.SingleAxisOpts{Type: "time", Bottom: "10%"},
)
tr.Add("themeRiver", trTime)
```
![](https://user-images.githubusercontent.com/19553554/52798246-7ebae400-30b2-11e9-8489-6c10339c3429.gif)