# S7 AI 通道常规处理子过程

## 说明

- 用于博途的SCL源码：AI_Proc(portal).scl
- 用于Step7的SCL源码：AI_Proc(step7).scl
- 用于PCS7的SCL源码：AI_Proc(pcs7).scl

## 调用示例

调用时，先建立对应的背景数据块，比如"TIT001"，调用时所有参数可省略，直接操纵背景块。

注：下方_name_表示具体变量

1. 在 TIA Portal 中调用示例：

    ```Pascal
    "TIT001"(
             AI:=0,                     // 模块采集值, 最好定义一个对应PIW通道的Int类型符号，以免除转换
             zero_raw:=0,               // 模块零点值（4mA对应数值）0
             span_raw:=27648,           // 模块量程值（20mA对应数值）27648
             overflow_SP:=28000,        // 上溢出值
             underflow_SP:=-500,        // 下溢出值
             zero:=0.0,                 // 量程低值
             span:=100.0,               // 量程高值
             invalid_value:=-1000000.0, // 无效输入时指定输出值
             AH_limit:=80.0,            // 高高报设定值
             WH_limit:=70.0,            // 高报设定值
             WL_limit:=2.0,             // 低报设定值
             AL_limit:=1.0,             // 低低报设定值
             dead_zone:=0.5,            // 死区 （赋值0.0时无死区）
             FT_time:=T#0MS,            // 容错时间 (单位毫秒 赋值T#0MS时无容错时间)
             PV=>_real_out_,            // 采集量工程单位数值
             AH_flag=>_bool_out_,       // 高高报标志
             WH_flag=>_bool_out_,       // 高报标志
             WL_flag=>_bool_out_,       // 低报标志
             AL_flag=>_bool_out_,       // 低低报标志
             invalid=>_bool_out_,       // 数据无效，即 AI_error OR overflow OR underflow
             AI_error=>_bool_out_,      // 非测量输入，比如断线
             overflow=>_bool_out_,      // 高溢出
             underflow=>_bool_out_,     // 低溢出
             SP_error=>_bool_out_);     // 设置错误
    ```

1. 在 Step7 V5.5 中SCL调用示例：

    ```Pascal
    AI_Proc.TIT001(
        AI                  := WORD_TO_INT(PIW256),      // 通道输入值，最好定义一个INT类型的PIW符号可不用转换
        zero_raw            := 0,                        // 通道零点值（4mA对应数值）0
        span_raw            := 27648,                    // 通道量程值（20mA对应数值）27648
        overflow_SP         := 28000,                    // 指定上溢出的容错通道值 默认28000
        underflow_SP        := -500,                     // 指定下溢出的容错通道值 默认-500
        zero                := 0.0,                      // 零点值
        span                := 100.0,                    // 量值
        invalid_value       := -1000000.0,               // 无效输入时指定输出值,比如回路断线
        AH_limit            := 100.0,                    // 高高报设定值
        WH_limit            := 100.0,                    // 高报设定值
        WL_limit            := 0.0,                      // 低报设定值
        AL_limit            := 0.0,                      // 低低报设定值
        dead_zone           := 0.5,                      // 死区 (赋值0.0时无死区)
        FT_time             := T#0MS)                    // 容错时间 (单位毫秒 赋值T#0MS时无容错时间)
    _real_out_ := TIT001.PV                              // 采集量工程单位数值
    _bool_out_ := TIT001.AH_flag;                        // 高高报标志
    _bool_out_ := TIT001.WH_flag;                        // 高报标志
    _bool_out_ := TIT001.WL_flag;                        // 低报标志
    _bool_out_ := TIT001.AL_flag;                        // 低低报标志
    _bool_out_ := TIT001.invalid                         // 数据无效
    _bool_out_ := TIT001.AI_error                        // 测量出错，比如断线
    _bool_out_ := TIT001.overflow;                       // 高溢出
    _bool_out_ := TIT001.underflow;                      // 低溢出
    _bool_out_ := TIT001.SP_error;                       // 报警值设置错误
    ```

1. 在 Step7 V5.5 中STL调用示例：

    ```Pascal
    CALL  "AI_Proc" , "TIT001"(
        AI                  := PIW256,            // 通道输入值，最好定义一个INT类型的PIW符号可不用转换
        zero_raw            := 0,                 // 通道零点值（4mA对应数值）0
        span_raw            := 27648,             // 通道量程值（20mA对应数值）27648
        overflow_SP         := 28000,             // 指定上溢出的容错通道值 默认28000
        underflow_SP        := -500,              // 指定下溢出的容错通道值 默认-500
        zero                := 0.0,               // 零点值
        span                := 100.0,             // 量值
        invalid_value       := -1000000.0,        // 无效输入时指定输出值,比如回路断线
        AH_limit            := 100.0,             // 高高报设定值
        WH_limit            := 100.0,             // 高报设定值
        WL_limit            := 0.0,               // 低报设定值
        AL_limit            := 0.0,               // 低低报设定值
        dead_zone           := 0.5,               // 死区 (赋值0.0时无死区)
        FT_time             := T#0MS,             // 容错时间 (单位毫秒 赋值T#0MS时无容错时间)
        PV                  := _real_out_,        // 采集量工程单位数值
        AH_flag             := _bool_out_,        // 高高报标志
        WH_flag             := _bool_out_,        // 高报标志
        WL_flag             := _bool_out_,        // 低报标志
        AL_flag             := _bool_out_,        // 低低报标志
        invalid             := _bool_out_,        // 数据无效
        AI_error            := _bool_out_,        // 测量出错，比如断线
        overflow            := _bool_out_,        // 高溢出
        underflow           := _bool_out_,        // 低溢出
        SP_error            := _bool_out_);       // 报警值设置错误
    ```
