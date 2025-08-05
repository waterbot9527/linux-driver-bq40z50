# bq40z50 Linux 驱动

> **注意**：由于 Linux 驱动可能稳定性不足，驱动程序的操作方法请参考 [这里](./README-old.md)，可以选择使用这里的python程序。

**如果要使用 python ，需要卸载bq40z50的驱动，将  树莓派中，将 /boot/config.txt 中的 dtoverlay=bq40z50-overlay 注释或删除**

## 一、使用 Python 程序读取或控制 bq40z50 状态

### 1. 将 `bq40z50` 文件夹复制到 `rpicm5`

请根据具体使用到的i2c修改指定的index是0或者其他: "smbus:0"

### 2. 常用指令示例
```bash
# 查看可读取的状态
./comm_sbs_bqctrl.py -v --bus "smbus:0" --dev_address 0x0b --chip BQ40z50 read-list

# 查看可操作的开关
./comm_sbs_bqctrl.py -v --bus "smbus:0" --dev_address 0x0b --chip BQ40z50 read-list
````

### 3. 在正常模式下无法打开电池充放电功能时，启用测试模式

```bash
# 关闭自动控制
./comm_sbs_bqctrl.py -v --bus "smbus:0" --dev_address 0x0b --chip BQ40z50 trigger ManufacturerBlockAccess.FETControl

# 打开充电模式
./comm_sbs_bqctrl.py -v --bus "smbus:0" --dev_address 0x0b --chip BQ40z50 trigger ManufacturerAccess.ChargeFET

# 打开放电模式
./comm_sbs_bqctrl.py -v --bus "smbus:0" --dev_address 0x0b --chip BQ40z50 trigger ManufacturerAccess.DischargeFET
```

> 根据谢总描述，之前无法正常打开的充放电模式后来可以使用了。
> 若再次无法使用，可参考 [测试模式](#3-在正常模式下无法打开电池充放电功能时启用测试模式)。
