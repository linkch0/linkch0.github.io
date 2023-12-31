---
date:
    created: 2022-02-03
    updated: 2023-12-31
slug: ffmpeg
authors: [linkchen]
categories: [Misc, Updating]
tags: [FFmpeg, Misc, Updating]
comments: true
---

# FFmpeg 笔记

[官方文档](https://ffmpeg.org/ffmpeg.html)

<!-- more -->

1. 查看 mkv 封装信息, `ffmpeg -i input.mkv`
2. mkv 只分离视频为 mp4, `ffmpeg -i input.mkv -vcodec copy -an output.mp4`
3. mkv 只分离音频为 flac, `ffmpeg -i input.mkv -acodec copy -vn output.flac`
4. flv 分离为 mp4, `ffmpeg -i input.flv -c copy output.mp4`
5. 提取 mp4 的音频为 mp3, `ffmpeg -i audio.mp4 -vn audio.wav/mp3`
6. 合并音频和视频文件，并使用 aac 重新编码音频文件, `ffmpeg -i video.mp4 -i audio.wav/mp3 -c:v copy -c:a aac output.mp4 `
