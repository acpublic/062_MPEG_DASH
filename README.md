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
### サンプル動画ダウンロード
```
wget https://download.blender.org/peach/bigbuckbunny_movies/BigBuckBunny_320x180.mp4 -O input.mp4
```

### ffmpegで映像のみ出力
```
ffmpeg -i input.mp4 -c:v libx264 -b:v 500k -an video.mp4
```
### ffmpegで音声のみ出力
```
ffmpeg -i input.mp4 -c:a aac -b:a 128k -vn audio.mp4
```
### ffmpegで音声のみ出力
```
ffmpeg -i input.mp4 -c:a aac -b:a 128k -vn audio.mp4
```
### MPEG-DASHに変換
```
MP4Box -dash 1000 -frag 1000 -rap -segment-name segment_ -out manifest.mpd video.mp4
```
- manifest.mpd
- segment_init.mp4
- segment_*.m4s
