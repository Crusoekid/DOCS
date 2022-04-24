# APS

### 📩APSRecive

#### 本地摄像头注册
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "insert"},
    { "mode", "camera"}
}
```

#### 本地图片注册
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "insert"},
    { "mode", "url"},
    { "data", url地址}
}
```

#### 平台下发注册
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "insert"},
    { "mode", "plantform"},
    { "data", {
        {"img_width", image_width},
        {"img_height", image_height},
        {"img_data", Enc_image}
            }
    }
}
```

#### 本地摄像头更新
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "update"},
    { "mode", "camera"}
}
```

#### 本地图片更新
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "update"},
    { "mode", "url"},
    { "data", url地址}
}
```

#### 平台下发更新
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "update"},
    { "mode", "plantform"},
    { "data", {
        {"img_width", image_width},
        {"img_height", image_height},
        {"img_data", Enc_image}
            }
    }
}
```

#### 删除数据所有注册信息
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "delete"},
    { "mode", "all"}
}
```

#### 删除指定image_id的信息
- Topic : ```aps.faceid_register_json.v1```
- 端口 : ```24101```
- 格式
```json
{
    { "msg_id", msg_id },
    { "img_id", img_id },
    { "action", "delete"},
    { "mode", "personal"}
}
```

#### 人脸操作行为
- Topic : ```aps.faceid_distinguish_json.v1```
- 端口 : ```24101```
- 格式
```json
{  
    { "action", "distinguish/selectall"} # 识别 / 查询数据库所有id
}
```

### 📤APSSend 

#### 注册信息回调
- Topic : ```aps.register_info_json.v1```
- 端口 : ```24100```
- 格式
```json
{  
    {"action", "insert/update/delete"},
    {"img_id", image_id},
    {"return", "failed/success"}, # 由于开始拼写错误，注意 failed
    {"msg_id", msg_id},
    {"id", IC_Card_id}
}
```

#### 人脸比对结果回调
- Topic : ```aps.distinguish_info_json.v1```
- 端口 : ```24100```
- 格式
```json
{
    {"faceid_mode", type}, # 识别类型字段(定速，定距，时间等待)
    {"status", "success/fail"},
    {"reason", "id_not_match/id_match/no_face"},
    {"driver_id", IC_Card_id},
    {"driver_name", 驾驶员名字},
    {"speed", 车速}, # double
    {"similarity", 相似度}, # 仅回调状态为success时拥有
    {"image_id", 当前相似度数据库匹配的image_id(唯一)} # 仅回调状态为success时拥有
}
```

#### 数据库查询结果
- Topic : ```aps.select_info_json.v1```
- 端口 : ```24100```
- 格式
```json
{  
    {"ids", 数据库image_id数组 (std::vector<std::string>)},
}
```

#### 天迈真疲劳检测
- Topic:  ```aps.realtired_msgpack.v1```
- 端口: ```24100```
- 格式:  
```json 
{  
    { "events", 告警事件 (std::vector<std::string>)},
    { "time_before_happen", 多少毫秒前发生的时间 (int 单位毫秒) }
}
```

#### 苏州创程定制化方案
- Topic: ```dms.core_alert.0x100```
- 端口:```24100```
- 格式:
```json
    {"aps",
        {
            {"frame_id", ctx.frame.count},
            {"time_ms", ctx.frame.millis},
            {"speed", ctx.vehicle_info.speed},
            {"alerts", 告警事件(std::vector<std::string>) }
        },
    }
```         

!>  alerts事件目前有： 起步左顾右盼```startlookaround```，进站左顾右盼```pittedlookaround```，转弯左顾右盼```turninglookaround```， 路口左顾右盼```intersectionlookaround```

## 📤APSCan
#### 成都昊岳Can输出
- topic: ```minieye.can_info_json.v1```
- 端口: ```24100```
```json
{
    "can_id": "0x0CFFBDE1",    # string
    "can" :  "can1/can2" ,     # string
    "customer" : "haoyue",     # string
    "can_data" : "base64_string" # unsigned char[8] base64 encode
}
```




# BSD

### 📤BSDSend 
- Topic : ```output.adas.warning```
- 端口 : ```24013```
- 格式
```json
{  
    { "event", "RBsdWarningL1/RBsdWarningL2/RBsdWarningL3/RBsdWarningNone"},
    { "transfer", "t01/t10"}, # 开始/结束
    { "speed", 车速 }, #double
    { "time", 时间} # int64_t 微秒
    { "warn_id", 1}
}
```

#### 📤物泊科技
- Topic : ```bsd.alert_msgpack.v1```
- 端口 : ```24013```
- 格式
```json
{  
    { "event", "ped/roll_over/bucket/tarpaulin/occation"},
    { "speed", 车速 }, #double
    { "time", 时间} # int64_t 微秒
}
```


## 📤BSDCan
- Topic : ```output.adas.algo```
- 端口 : ```24013```
- 格式
```json
{  
    { "msg_type", "bsd_warning"},
    { "frame_id", Frame ID},
    { "camera_time", time}, # us
    { "host_speed", speed},
    { "time", time }, # us
    { "bsd_warning_l1_on", 0/1},
    { "bsd_warning_l2_on", 0/1},
    { "bsd_warning_l3_on", 0/1},
    { "bsd_warning_chaned", bsd告警状态改变}
}
```     
!> 需要配置/sdcard/run/bsd_setup.flag --enable_bsd_can_info_upload=true


# FBSD
- Topic : ```output.adas.warning```
- 端口 : ```24013```
- 格式
```json
{  
    { "event", "FBsdWarning/FBsdWarningNone"},
    { "transfer", t01/t10 } #开始和结束
}
```

# HOD

### 📤HODSend 
- Topic : ```hod.alert_info_json.v1```
- 端口 : ```24024```
- 格式
```json
    {
        "hod",
        {
            {"frame_id", frame_id},
            {"time_ms", 时间}, # 毫秒
            {"speed", 车速},
            {"alerts", 告警事件} # handsoff/singlehandoff
        }
    }
```