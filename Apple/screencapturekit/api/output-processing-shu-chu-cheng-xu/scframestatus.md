# SCFrameStatus

```
public enum SCFrameStatus : Int, @unchecked Sendable {
    case complete = 0 // 帧率生成
    case idle = 1 // 新的帧率没有生成，因为display没有改变
    case blank = 2 // 新的帧率没有生成，因为display是空的
    case suspended = 3 //新的帧率没有生成，因为更新已经悬挂
    case started = 4 //被指示为在流已经开始之后发送的第一帧的新帧。
    case stopped = 5 // 流已经停止
}

```
