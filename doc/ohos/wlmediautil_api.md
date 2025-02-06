## WlMediaUtil API
WlMediaUtil 是一个获取 `音视频基础信息` 和获取 `缩略图` SDK，其使用方法如下：
### 一 构造函数
`WlMediaUtil` 构造函数不依赖上下文，很方便创建使用，当创建了 `WlMediaUtil` 实例后，都需要调用 `release` 释放资源。
#### 1.1 无参构造函数
```typescript
public WlMediaUtil()
```

### 二 常用方法
#### 2.1 设置FF参数
有些网络流，如 `rtsp` 流需要设置使用 `tcp` 或 `udp` 网络模式才能播放，设置方式如下：
##### 2.1.1 设置参数
```typescript
public setOptions(key: string, value: string)
```
##### 2.1.2 清除所有参数
```typescript
public clearOptions()
```

#### 2.2 设置网络资源访问超时时长
设置访问网络资源超时时长，默认 15s。
##### 2.2.1 设置超时时间
```typescript
public setTimeOut(timeOut: number)
```

#### 2.3 设置数据源
```typescript
public setSource(source: string)
```

#### 2.4 打开资源
```typescript
/**
 * 打开 数据源
 *
 * @return 0：success
 * -1: 超时
 * -2: 错误
 */
public openSource(): number
```

#### 2.5 获取音视频信息
##### 2.5.1 获取所有音频信息
```typescript
public getAudioTracks(): WlTrackInfoBean[] | undefined
```
##### 2.5.2 获取所有视频信息
```typescript
public getVideoTracks(): WlTrackInfoBean[] | undefined
```
##### 2.5.3 获取所有字幕信息
```typescript
public getSubtitleTracks(): WlTrackInfoBean[] | undefined
```

#### 2.6 获取缩略图
```typescript
/**
 * 获取对应时间截图
 *
 * @param trackIndex  获取截图的视频track
 * @param time        如果 time > 0 , 就会取time对应的时间值，如果 time = 0，会按照顺序依次读取截图
 * @param keyFrame    表示是不是只取关键帧（关键帧速度快）
 * @param scaleWidth  缩放宽
 * @param scaleHeight 缩放高
 * @return
 */
public getVideoFrame(trackIndex: number, time: number, keyFrame: boolean, scaleWidth: number,
    scaleHeight: number): image.PixelMap | null
```

#### 2.7 销毁资源
只要创建了实例，就要调用release销毁。
```typescript
public release()
```

### 三 注意事项
`WlMediaUtil` 中 `openSource`、`getVideoFrame` 都是`线程阻塞`方法，需要在`子线程中调用`，才`不会阻塞主线程`。