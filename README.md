# lalmax
lalmax是以lal为内核的卍解

# 编译
./build.sh

# 运行
./run.sh或者./lalmax -c conf/lalmax.conf.json

# 配置说明
lalmax.conf.json配置主要由2部分组成

(1) lal_config_path表示lal配置文件的路径,用于加载lal本身的配置,具体配置说明见[lal配置](https://pengrl.com/lal/#/ConfigBrief)

(2) 剩余的配置则为lalmax的配置,具体配置说明见[config.md](./document/config.md)


# docker运行
```
docker build -t lalmax:init ./

docker run -it -p 1935:1935 -p 8080:8080 -p 4433:4433 -p 5544:5544 -p 8083:8083 -p 8084:8084 -p 30000-30100:30000-30100/udp -p 1290:1290 -p 6001:6001/udp lalmax:init

```

# 架构

![图片](image/init.png)

# 支持的协议
## 推流
(1) RTSP 

(2) SRT

(3) RTMP

(4) RTC(WHIP)

(5) GB28181

具体的推流url地址（除了srt/whip）

https://pengrl.com/lal/#/streamurllist

## 拉流
(1) RTSP

(2) SRT

(3) RTMP

(4) HLS(S)-TS

(5) HTTP(S)-FLV

(6) HTTP(S)-TS

(7) RTC(WHEP)

(8) HTTP(S)-FMP4

(9) HLS(S)-FMP4/LLHLS


具体的拉流url地址见https://pengrl.com/lal/#/streamurllist（除了srt/whep）

## [SRT](./document/srt.md)
（1）使用gosrt库

（2）暂时不支持SRT加密

（3）支持H264/H265/AAC

（4）可以对接OBS/VLC

推流url
srt://127.0.0.1:6001?streamid=publish:test110

拉流url
srt://127.0.0.1:6001?streamid=test110

## [WebRTC](./document/rtc.md)
（1）支持WHIP推流和WHEP拉流,暂时只支持POST信令

（2）支持H264/G711A/G711U,后续支持opus音频

（3）可以对接OBS、vue-wish

WHIP推流url
http(s)://127.0.0.1:1290/whip?streamid=test110

WHEP拉流url
http(s)://127.0.0.1:1290/whep?streamid=test110

## Http-fmp4
(1) 支持H264/H265/AAC/G711A/G711U

拉流url
http(s)://127.0.0.1:1290/live/m4s/test110.mp4

## HLS(fmp4/Low Latency)
(1) 支持H264/H265/AAC

拉流url
http(s)://127.0.0.1:1290/live/hls/test110/index.m3u8

## [GB28181](./document/gb28181.md)
(1) 作为SIP服务器与设备进行SIP交互,打开lalserver的端口接收码流

(2) 流ID为设备通道编码ID

(3) 支持H264/H265/AAC

(4) 支持TCP/UDP



