# 上位机与Lite通讯JSON文档

## 说明
JSON标识 | 英语注释 | 中文注释 | 类型 |备注
:---|:---|:---|:---|:---
**id** | Unique_ID | 地址编号 | 整型 |
**did** | Device_Unique_ID | 设备编号 | 整型 |
**dt** | Device_type | 设备种类 | 整型 | 1:DLT645 2: Modbus TCP
**fc** | Function_Code | 功能码 | 字符串 | 读设备gd，读值gv，写值pv,新写地址pa, 新写设备pd, 修改地址ma，修改设备md，删除地址da，删除设备dd
**fa** | fromAddress | 读取远程设备的地址 | 字符串 |
**ta** | toAddress | 存储本地Lite的地址 | 字符串 |
**dadd** | DeviceAddress | 读取设备的地址 | 字符串 | ModbusTCP:DeviceAddress Dlt645:12位编码
**s** | Status_Code | 通讯状态 | 整型 | OK:200 Erorr:400

## Dlt645设备报文格式(JSON)

* 新增设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "dadd":"DeviceAddress"}
{"fc":"pd", "dt":"1", "dadd":"20188888888888"}
```

* 新增设备（Lite发送到上位机）

```json
{"s":"Status_Code",  "did":"Device_Unique_id"}
{"s":"200",  "did":"1001"}，{"s":"400"}
```

* 修改设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "dadd":"DeviceAddress"}
{"fc":"md", "dt":"1", "did":"1001", "dadd":"20187777777777"}
```

* 修改设备（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 删除设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id"}
{"fc":"dd", "dt":"1", "did":"1001"}
```

* 删除设备（Lite发送到上位机）
```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 读取设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id"}
{"fc":"gd", "dt":"1", "did":"-1"}
```

* 读取设备（Lite发送到上位机）

```json
{
  "s": "Status_Code",
  "data": {
    "Device_Unique_id": "DeviceAddress",
  }
}
{
  "s": "200",
  "data": {
    "1001": "20181234554321",
    "1002": "2018123455432",
    "1003": "20181234554323",
    "1004": "20181234554324"
  }
}
```

* 新增地址（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "fa":"fromAddress"}
{"fc":"pa", "dt":"1", "did":"1001", "fa":"060504030201"}
```

* 新增地址（Lite发送到上位机）

```json
{"s":"Status_Code", "id":"Unique_id", "ta":"toAddress"}
{"s":"200", "id":"0001", "ta":"30001:2"}，{"s":"400"}
```

* 修改地址（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "id":"Unique_id", "fa":"fromAddress"}
{"fc":"ma", "dt":"1", "did":"1001", "id":"0001", "fa":"070504030207"}
```

* 修改地址（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 删除地址（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "id":"Unique_id"}
{"fc":"da", "dt":"1", "did":"1001", "id":"0001"}
```

* 删除地址（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 读取值（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id"}
{"fc":"gv", "dt":"1", "did":"1001"}
```

* 读取值（Lite发送到上位机）

```json
{
  "s": "Status_Code",
  "data": [
    {
      "id": "Unique_id",
      "fa": "fromAddress",
      "ta": "toAddress",
      "v": "value"
    }]
}

{
  "s": "200",
  "data": [
    {
      "id": "0001",
      "fa": "070504030207",
      "ta": "30001:2",
      "v": "35.22"
    },
    {
      "id": "0002",
      "fa": "070504030208",
      "ta": "30003:2",
      "v": "57.64"
    }
  ]
}
```

## Modbus TCP设备报文格式(JSON)

* 新增设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "dadd":"DeviceAddress"}
{"fc":"pd", "dt":"2", "dadd":"192.168.0.77:5002:1"}
```

* 新增设备（Lite发送到上位机）

```json
{"s":"Status_Code",  "did":"Device_Unique_id"}
{"s":"200",  "did":"2001"}，{"s":"400"}
```

* 修改设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "dadd":"DeviceAddress"}
{"fc":"md", "dt":"2", "did":"2001", "dadd":"192.168.0.99:5002:2"}
```

* 修改设备（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 删除设备（上位机发送到Lite）

```json
{"fc":"Function_Code", "did":"Device_Unique_id"}
{"fc":"dd", "dt":"2", "did":"2001"}
```

* 删除设备（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 设备读取（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id"}
{"fc":"gd", "dt":"2", "did":"-1"}
```

* 设备读取（Lite发送到上位机）

```json
{
  "s": "Status_Code",
  "data": {
    "Device_Unique_id": "DeviceAddress"
  }
}
{
  "s": "200",
  "data": {
    "2001": "192.168.0.77:5002:1",
    "2002": "192.168.0.78:5002:1",
    "2003": "192.168.0.79:5002:1"
  }
}
```

* 新增地址（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "fa":"fromAddress"}
{"fc":"pa", "dt":"2", "did":"2001", "fa":"16:40001:2"}
```

* 新增地址（Lite发送到上位机）

```json
{"s":"Status_Code", "id":"Unique_id", "ta":"toAddress"}
{"s":"200", "id":"0001", "ta":"41001:2"}，{"s":"400"}
```

* 修改地址（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "id":"Unique_id", "fa":"fromAddress"}
{"fc":"ma", "dt":"2", "did":"2001", "id":"0001", "fa":"16:40011:2"}
```

* 修改地址（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 删除地址（上位机发送到Lite）

```json
{"fc":"Function_Code",  "dt":"Device_Type", "did":"Device_Unique_id", "id":"Unique_id"}
{"fc":"da", "dt":"2", "did":"2001","id":"0001"}
```

* 删除地址（Lite发送到上位机）

```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

* 读取值（上位机发送到Lite）

```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id"}
{"fc":"gv", "dt":"2", "did":"2001"}
```

* 读取值（Lite发送到上位机）

```json
{"id":"Unique_id", "fa":"fromAddress", "ta":"toAddress", "v":"value"}
{
  "s": "Status_Code",
  "data": [
    {
      "id": "Unique_id",
      "fa": "fromAddress",
      "ta": "toAddress",
      "v": "value"
    }]
}{
  "s": "200",
  "data": [
    {
      "id": "0001",
      "fa": "16:40100:2",
      "ta": "41100:2",
      "v": "135.22"
    },
    {
      "id": "0002",
      "fa": "16:40102:2",
      "ta": "41102:2",
      "v": "157.64"
    }
  ]
}
```

-----------------------------------

## 通讯流程(电表)

1. 上位机传数据fromAddress给Lite
2. Lite分配本地Modbus地址
3. Lite将fromAddress与toAddress配对存储到本地数据库或文件
4. Lite将数据toAddress传回给上位机

重复fromAddress的问题
判断40001:2是否跟2的问题 左没有2 右有2

## Modbus功能码

功能码 | Register Type | 名称
:---:|:---|:---
1 | Read Coil | 读取线圈状态
2 | Read Discrete Input | 读取输入状态
3 | Read Holding Registers | 读取保持寄存器
4 | Read Input Registers | 读取输入寄存器
5 | Write Single Coil | 强置单线圈
6 | Write Single Holding Register | 预置单寄存器
15| Write Multiple Coils | 强置多线圈
16| Write Multiple Holding Registers | 预置多寄存器

## Modbus寄存器说明

寄存器种类 | 说明 | PLC类比 | 举例说明
:---|:---|:---|:---
线圈状态 | 输出端口。可设定端口的输出状态，也可以读取该位的输出状态。可分为两种不同的执行状态，例如保持型或边沿触发型。 | DO 数字量输出 | 电磁阀输出，MOSFET输出，LED显示等。
离散输入状态|输入端口。通过外部设定改变输入状态，可读但不可写。|DI数字量输入|拨码开关，接近开关等。
保持寄存器|输出参数或保持参数，控制器运行时被设定的某些参数。可读可写。|AO模拟量输出|模拟量输出设定值，PID运行参数，变量阀输出大小，传感器报警上限下限。
输入寄存器|输入参数。控制器运行时从外部设备获得的参数。可读但不可写。|AI模拟量输入|模拟量输入

## Modbus寄存器地址分配

寄存器PLC地址|寄存器协议地址|适用功能|寄存器种类|读写状态
:---|:---|:---|:---|:---
00001-09999|0000H-FFFFH|01H 05H 0FH|线圈状态|可读可写
10001-19999|0000H-FFFFH|02H|离散输入状态|可读
30001-39999|0000H-FFFFH|04H|输入寄存器|可读
40001-49999|0000H-FFFFH|03H 06H 0FH|保持寄存器|可读可写

## DLT645地址

名称 | Measurement Type | 地址
:---|:---|:---
电压 | PHASE_A_VOLTAGE | 0x02010100
电流 | PHASE_A_CURRENT | 0x02020100
频率 | METER_FREQUENCY | 0x02800002
功率因数 | PHASE_TOTAL_POWER_FACTOR | 0x02060000
电能 | POSITIVE_ACTIVE_TOTAL_ENERGY | 0x00000000