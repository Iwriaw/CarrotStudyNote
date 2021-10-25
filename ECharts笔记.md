# ECharts学习笔记
## 图表容器及大小
图表的容器一般为一个指定大小的div，若不指定图表大小，图表的大小与容器大小一致。

需要注意的是，使用这种方法在调用 echarts.init 时需保证容器已经有宽度和高度了。
### 响应容器大小的变化
在有些场景下，我们希望当容器大小改变时，图表的大小也相应地改变。

这种情况下，可以监听页面的 window.onresize 事件获取浏览器大小改变的事件，然后调用 echartsInstance.resize 改变图表的大小。

<style>
```js
<script type="text/javascript">
  var myChart = echarts.init(document.getElementById('main'));
  window.onresize = function() {
    myChart.resize();
  };
</script>
```