# 上位机与Lite通讯JSON文档

## 说明
JSON标识 | 英语注释 | 中文注释 | 备注
:---|:---|:---|:---
**id** | Unique_ID | 地址编号 |
**did** | Device_Unique_ID | 设备编号 |
**dt** | Device_type | 设备种类 | 1:DLT645 2: Modbus TCP
**fc** | Function_Code | 功能码 |读rr，新写地址pa, 新写设备pd, 修改地址ma，修改设备md，删除地址da，删除设备dd
**fa** | fromAddress | 读取远程设备的地址 |
**ta** | toAddress | 存储本地Lite的地址 |
**dadd** | DeviceAddress | 读取设备的地址 | ModbusTCP:DeviceAddress Dlt645:12位编码
**s** | Status_Code | 通讯状态 | OK:200 Erorr:400


# Dlt645设备报文格式(JSON)

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



* 新增地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "dt":"Device_Type", "fa":"fromAddress"}
{"fc":"pa", "dt":"1", "fa":"060504030201"}
```
* 新增地址（Lite发送到上位机）
```json
{"s":"Status_Code", "id":"Unique_id", "ta":"toAddress"}
{"s":"200", "id":"0001", "ta":"30001:2"}，{"s":"400"}
```
* 修改地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "dt":"Device_Type", "id":"Unique_id", "fa":"fromAddress"}
{"fc":"ma", "dt":"1", "id":"0001", "fa":"070504030207"}
```
* 修改地址（上位机发送到Lite）
```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```
* 删除地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "dt":"Device_Type", "id":"Unique_id"}
{"fc":"da", "dt":"1", "id":"0001"}
```
* 删除地址（上位机发送到Lite）
```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```

# Modbus TCP设备报文格式(JSON)

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

* 新增地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "dt":"Device_Type", "did":"Device_Unique_id", "fa":"fromAddress"}
{"fc":"pa", "dt":"2", "fa":"40001:2"}
```
* 新增地址（Lite发送到上位机）
```json
{"s":"Status_Code", "id":"Unique_id", "ta":"toAddress"}
{"s":"200", "id":"0001", "ta":"41001:2"}，{"s":"400"}
```
* 修改地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "did":"Device_Unique_id", "id":"Unique_id", "fa":"fromAddress"}
{"fc":"ma", "dt":"2", "id":"0001", "fa":"40011:2"}
```
* 修改地址（Lite发送到上位机）
```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```
* 删除地址（上位机发送到Lite）
```json
{"fc":"Function_Code",  "did":"Device_Unique_id", "id":"Unique_id"}
{"fc":"da", "dt":"2", "id":"0001"}
```
* 删除地址（Lite发送到上位机）
```json
{"s":"Status_Code"}
{"s":"200"}，{"s":"400"}
```
-----------------------------------


### 通讯流程(电表)
1. 上位机传数据fromAddress给Lite
2. Lite分配本地Modbus地址
3. Lite将fromAddress与toAddress配对存储到本地数据库或文件
4. Lite将数据toAddress传回给上位机


重复fromAddress的问题
判断40001:2是否跟2的问题 左没有2 右有2