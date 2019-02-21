# 上位机与Lite通讯JSON文档

## 说明
JSON标识 | 英语注释 | 中文注释 | 备注
:---|:---|:---|:---
**d** | Device | 设备种类 | 1:DLT645 2: Modbus TCP
**fc** | Function Code | 功能码 |读ff，新写rr, 修改mm，删除dd
**f** | fromAddress | 读取远程设备的地址 |
**t** | toAddress | 存储本地Lite的地址 |
**ip** | IpFrom | 读取设备的ip:socket:device_id |

## 格式
```json
{"d":"1", "fc":"ff","f":"fromAddress","t":"toAddress"}
```

## 列子
### dlt645设备： 
```json
{"d":"1","fc":"ff","f":"201888888888","t":"41001"}
```
### Modbus Tcp设备： 
```json
{"d":"2", "ip":"192.168.1.1:5002:01","fc":"ff","f":"04:40001:5","t":"400010:5"}
```
### 通讯流程
1. 电表为例上位机传数据给Lite，JSON如下:
```json
{"d":"1","fc":"ff","f":"201888888888","t":""}
```
2. Lite分配本地Modbus地址
3. Lite将DeviceFrom与DeviceTo配对存储到本地数据库或文件
4. Lite将数据传回给上位机，JSON如下:
```json
{"d":"1","fc":"ff","f":"20188888888","t":"41001"}
```