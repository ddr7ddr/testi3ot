# 上位机与Lite通讯JSON文档

## 说明
JSON标识 | 英语注释 | 中文注释 | 备注
:---|:---|:---|:---
**id** | Unique_ID | 地址编号 |
**did** | Device_Unique_ID | 设备编号 |
**d** | Device_type | 设备种类 | 1:DLT645 2: Modbus TCP
**fc** | Function_Code | 功能码 |读rr，新写地址pa,新写设备pd,修改地址ma，修改设备md，删除地址da，删除设备dd
**f** | fromAddress | 读取远程设备的地址 |
**t** | toAddress | 存储本地Lite的地址 |
**ip** | IpFrom | 读取设备的ip:socket:device_id |
**s** | Status_Code | 通讯状态 | OK:200 Erorr:400


# Dlt645设备报文格式(JSON)
* 新增地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "d":"Device_Type", "f":"fromAddress"}
```
* 新增地址（Lite发送到上位机）
```json
{"s":"Status_Code", "id":"Unique_id", "t":"toAddress"}
```
* 修改地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "id":"Unique_id", "f":"fromAddress"}
```
* 修改地址（上位机发送到Lite）
```json
{"s":"Status_Code"}
```
* 删除地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "id":"Unique_id"}
```
* 删除地址（上位机发送到Lite）
```json
{"s":"Status_Code"}
```

# Modbus TCP设备报文格式(JSON)

* 新增设备（上位机发送到Lite）
```json
{"fc":"Function_Code", "d":"Device_Type", "ip":"ip_address:socket:device_id"}
```
* 新增设备（Lite发送到上位机）
```json
{"s":"Status_Code",  "did":"Device_Unique_id"}
```
* 修改设备（上位机发送到Lite）
```json
{"fc":"Function_Code", "did":"Device_Unique_id", "ip":"ip_address:socket:device_id"}
```
* 修改设备（Lite发送到上位机）
```json
{"s":"Status_Code"}
```
* 删除设备（上位机发送到Lite）
```json
{"fc":"Function_Code", "did":"Device_Unique_id"}
```
* 删除设备（Lite发送到上位机）
```json
{"s":"Status_Code"}
```

* 新增地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "d":"Device_Type", "did":"Device_Unique_id", "f":"fromAddress"}
```
* 新增地址（Lite发送到上位机）
```json
{"s":"Status_Code", "id":"Unique_id", "t":"toAddress"}
```
* 修改地址（上位机发送到Lite）
```json
{"fc":"Function_Code", "did":"Device_Unique_id", "id":"Unique_id", "f":"fromAddress"}
```
* 修改地址（Lite发送到上位机）
```json
{"s":"Status_Code"}
```
* 删除地址（上位机发送到Lite）
```json
{"fc":"Function_Code",  "did":"Device_Unique_id", "id":"Unique_id"}
```
* 修改地址（Lite发送到上位机）
```json
{"s":"Status_Code"}
```
-----------------------------------


### 通讯流程(电表)
1. 上位机传数据fromAddress给Lite
2. Lite分配本地Modbus地址
3. Lite将fromAddress与toAddress配对存储到本地数据库或文件
4. Lite将数据toAddress传回给上位机