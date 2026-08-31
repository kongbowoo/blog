# Linux perf 学习笔记

> 概述：`perf` 是 Linux 内核自带的性能分析工具，基于 PMU（性能监控单元）采集硬件计数器与软件事件，可用于定位 CPU 热点函数、分析 cache miss、分支预测失败等性能问题。

## 参考资源

- Perf 示例与教程（Brendan Gregg）：<http://www.brendangregg.com/perf.html>

## perf 事件图

perf 支持的软硬件事件全景图：

![perf的事件图](http://www.brendangregg.com/perf_events/perf_events_map.png)

## 常用命令速记

```shell
# 实时查看系统级 CPU 热点
perf top

# 采样指定命令的执行，生成性能统计
perf stat ./your_program

# 采样并记录调用栈数据
perf record -g ./your_program

# 以火焰图形式分析热点（需配合 FlameGraph 工具）
perf script | stackcollapse-perf.pl | flamegraph.pl > flame.svg
```

## 相关笔记

- [性能优化记录](../性能优化记录.md)
- [DDoS 防御性能优化小结](./DDoS防御性能优化小结.md)
