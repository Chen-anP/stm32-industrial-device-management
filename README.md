# STM32 工业互联设备管理系统

基于 STM32H563 中控和 STM32F030 传感节点的嵌入式固件工程，包含 FreeRTOS 多任务、Modbus RTU 通信、寄存器点表映射和 IAP 固件传输相关实现。

## 目录

| 目录 | 内容 |
| --- | --- |
| `02_中控程序/h5_iap/demo` | STM32H563RIVx 中控工程，包含 USB CDC、两路 UART/RS485 通信、点表管理与固件转发 |
| `03_传感器程序/f030_iap/f030_iap/demo` | STM32F030CCTx 传感节点工程，包含节点数据处理、Modbus 从站与 IAP |

当前仓库只包含中控与传感器固件，上位机程序不在本次目录中。

## 工程入口

使用 Keil MDK / µVision 打开对应工程，两个工程的 Target 名称均为 `demo`：

- 中控：[`02_中控程序/h5_iap/demo/MDK-ARM/demo.uvprojx`](02_中控程序/h5_iap/demo/MDK-ARM/demo.uvprojx)
- 节点：[`03_传感器程序/f030_iap/f030_iap/demo/MDK-ARM/demo.uvprojx`](03_传感器程序/f030_iap/f030_iap/demo/MDK-ARM/demo.uvprojx)

安装匹配器件的 STM32 Device Family Pack，并按板卡、启动模式核对 Flash/SRAM 布局后编译。工程内的 `.ioc`、链接脚本 `.sct`、启动文件、HAL/CMSIS 驱动和第三方库均保留。

工程构建后调用 `fromelf` 生成应用 `.bin` 文件，用于固件传输。生成的二进制文件由 `.gitignore` 排除，需要时在本地重新构建。

## 版本管理范围

上传源码、工程配置、驱动依赖、文档与第三方许可证。忽略编译中间文件、烧录产物、Keil 用户配置、编辑器缓存、日志和临时文件；本地文件不会因此被删除。

CMSIS 中的预编译 `.a`、`.lib` 是 SDK 依赖，保留在仓库中。`MDK-ARM/demo` 下的 `.sct` 链接脚本也保留，不将整个输出目录一并忽略。

## 第三方组件

工程包含 ST HAL/CMSIS、FreeRTOS、USBX、libmodbus 等组件。各文件的原作者、版权声明及现有许可证按原目录保留；第三方代码遵循各自的许可条件。
