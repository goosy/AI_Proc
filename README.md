# S7 AI 通道常规处理子过程

## 说明

- 用于博途的SCL源码：AI_Proc(Portal).scl
- 用于Step7的SCL源码：AI_Proc(step7).scl
- 用于Step7的STL源码：AI_Proc.AWL

## 调用示例

调用时，先建立对应的背景数据块，比如"TIT001"，调用时所有参数可省略，直接操纵背景块。

1. 在 TIA Portal 中调用示例：

    ```Pascal
    "TIT001"(analog_raw:="AI01-1",        // %IW256:P 通道输入值
             zero_raw:=0,                 // 变送器零点原始值（4mA对应数值）0
             span_raw:=27648,             // 变送器极值原始值（20mA对应数值）27648
             overflow_radius:=500,        // 指定溢出的容错值 默认500
             range_low:=0.0,              // 量程低值
             range_high:=100.0,           // 量程高值
             offset:=0.0,                 // 偏置值
             invalidValue:=-1000000.0,    // 无效输入时指定输出值,比如回路断线
             highAlarm:=80.0,             // 高高报设定值
             highWarn:=70.0,              // 高报设定值
             lowWarn:=2.0,                // 低报设定值
             lowAlarm:=1.0,               // 低低报设定值
             dead_zone_radius:=0.5,       // 死区半径 (赋值0.0时无死区)
             fault_tolerance_time:=T#0MS, // 容错时间 (单位毫秒 赋值T#0MS时无容错时间)
             PV=>_real_out_,              // 采集量工程单位数值
             highAlarm_flag=>_bool_out_,  // 高高报标志
             highWarn_flag=>_bool_out_,   // 高报标志
             lowWarn_flag=>_bool_out_,    // 低报标志
             lowAlarm_flag=>_bool_out_,   // 低低报标志
             highOverflow=>_bool_out_,    // 高溢出
             lowOverflow=>_bool_out_,     // 低溢出
             error=>_bool_out_);          // 错误
    ```

1. 在 Step7 V5.5 中调用SCL示例：

    ```Pascal
    AI_Proc.TIT001(
         analog_raw          := PIW256,      // 通道输入值
         zero_raw            := ,            // 变送器零点原始值（4mA对应数值）0
         span_raw            := ,            // 变送器极值原始值（20mA对应数值）27648
         overflow_radius     := ,            // 指定溢出的容错值 默认500
         range_low           := ,            // 量程低值
         range_high          := ,            // 量程高值
         offset              := ,            // 偏置值
         invalidValue        := ,            // 无效输入时指定输出值,比如回路断线
         highAlarm           := ,            // 高高报设定值
         highWarn            := ,            // 高报设定值
         lowWarn             := ,            // 低报设定值
         lowAlarm            := ,            // 低低报设定值
         dead_zone_radius    := ,            // 死区半径 (赋值0.0时无死区)
         fault_tolerance_time:= )            // 容错时间 (单位毫秒 赋值T#0MS时无容错时间)
    PV := TIT001.PV                          //采集量工程单位数值
    highAlarm_flag := TIT001.highAlarm_flag; //高高报标志
    highWarn_flag := TIT001.highWarn_flag;   //高报标志
    lowWarn_flag := TIT001.lowWarn_flag;     //低报标志
    lowAlarm_flag := TIT001.lowAlarm_flag;   //低低报标志
    highOverflow := TIT001.highOverflow;     //高溢出
    lowOverflow := TIT001.lowOverflow;       //低溢出
    error := TIT001.error;                   //错误
    ```

1. 在 Step7 V5.5 中调用STL示例：

    ```Pascal
    CALL  "AI_Proc" , "TIT001"(
       analog_raw          := PIW256, // 可只赋参数
       zero_raw            := , // 变送器零点原始值（4mA对应数值）0
       span_raw            := , // 变送器极值原始值（20mA对应数值）27648
       overflow_radius     := , // 指定溢出的容错值 默认500
       range_low           := , // 量程低值
       range_high          := , // 量程高值
       offset              := , // 偏置值
       invalidValue        := , // 无效输入时指定输出值,比如回路断线
       highAlarm           := , // 高高报设定值
       highWarn            := , // 高报设定值
       lowWarn             := , // 低报设定值
       lowAlarm            := , // 低低报设定值
       dead_zone_radius    := , // 死区半径 (赋值0.0时无死区)
       fault_tolerance_time:= , // 容错时间 (单位毫秒 赋值T#0MS时无容错时间)
       PV                  := , // 采集量工程单位数值
       highAlarm_flag      := , // 高高报标志
       highWarn_flag       := , // 高报标志
       lowWarn_flag        := , // 低报标志
       lowAlarm_flag       := , // 低低报标志
       highOverflow        := , // 高溢出
       lowOverflow         := , // 低溢出
       error               := ) // 错误
    ```
