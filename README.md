## MPEG-DASH
### 拡張子（マニフェスト）
- .mpd
### セグメント
- .m4s

## MPEG-DASHコンテンツ生成
### FFmpeg インストール
```
sudo apt install ffmpeg
```
### MP4Box（GPAC）のインストール
```
sudo apt install gpac
```
### サンプル動画ダウンロード(stream内で実施)
```
wget https://download.blender.org/peach/bigbuckbunny_movies/BigBuckBunny_320x180.mp4 -O input.mp4
```
## MPEG-DASHに変換（固定ビットレート）
### ffmpegで映像のみ出力
```
ffmpeg -i input.mp4 -c:v libx264 -b:v 500k -an video.mp4
```
### ffmpegで音声のみ出力
```
ffmpeg -i input.mp4 -c:a aac -b:a 128k -vn audio.mp4
```
### MP4Boxで変換
```
MP4Box -dash 1000 -frag 1000 -rap -segment-name segment_ -out manifest.mpd video.mp4#video audio.mp4#audio
```
- manifest.mpd
- segment_init.mp4
- segment_*.m4s

## MPEG-DASHに変換（平均ビットレート）
### ffmpegで各解像度でエンコード
```
ffmpeg -i input.mp4 -vf scale=640:360 -c:v libx264 -b:v 1000k -c:a aac -b:a 96k -y video_360.mp4
ffmpeg -i input.mp4 -vf scale=1280:720 -c:v libx264 -b:v 3000k -c:a aac -b:a 128k -y video_720.mp4
ffmpeg -i input.mp4 -vf scale=1920:1080 -c:v libx264 -b:v 5000k -c:a aac -b:a 192k -y video_1080.mp4
```
### MP4Boxで変換
```
MP4Box -dash 4000 -frag 4000 -rap -profile dashavc264:live -out manifest.mpd \
  video_360.mp4#video video_360.mp4#audio \
  video_720.mp4#video video_720.mp4#audio \
  video_1080.mp4#video video_1080.mp4#audio
```
- manifest.mpd
- video_360.mp4
- video_360_dash_track1_init.mp4
- video_360_dash_track1_*.m4s
- video_360_dash_track2_*.m4s
- video_720.mp4
- video_720_dash_track1_init.mp4
- video_720_dash_track1_*.m4s
- video_720_dash_track2_*.m4s
- video_1080.mp4
- video_1080_dash_track1_init.mp4
- video_1080_dash_track1_*.m4s
- video_1080_dash_track2_*.m4s
