---
layout: post
title: "从STEP脉冲理解ESP32的LEDC"
date: 2026-08-11 14:00:00 +0800
categories: [ESP32, 电机控制]
tags: [LEDC, PWM, TMC2209]
---

## 实验目的

使用ESP32-S3的LEDC外设产生STEP脉冲，驱动TMC2209。

## 硬件连接

| ESP32-S3 | TMC2209 |
|---|---|
| GPIO4 | STEP |
| GPIO5 | DIR |
| GPIO6 | EN |

## 我的理解

LEDC定时器负责产生计数时基，通道负责选择GPIO、占空比和输出相位。

## 实验结果

当STEP频率为10000Hz，驱动器配置为1/8微步时，理论转速为：

\[
n = \frac{10000}{200 \times 8} \times 60
= 375\text{ RPM}
\]

## 遇到的问题

最初程序把`ledc_set_freq()`的返回值误认为实际频率，导致程序触发错误检查并不断重启。

## 总结

这次实验让我理解了STEP频率、细分数和电机转速之间的关系。
