# Media Source demo

## Video encoding

```bash
$ ffmpeg -rtsp_transport tcp -i inputURL -f segment -segment_format mp4 -segment_format_options movflags=frag_keyframe+empty_moov+default_base_moof -segment_time 10 -strftime 1 -c:v copy test-%Y-%m-%dT%H-%M-%S.mp4
```

- `-f segment` - automatically segment the output files into individual files
- `-segment_format_options movflags=frag_keyframe+empty_moov+default_base_moof` - required for MSE to work properly in chrome
- `-segment_time 10` - split files into 10s chunks
- `-strftime 1` - allows the use of time format specifiers in the output filename
- `-c:v copy` - copy the video stream instead of re-encoding it

## Media Source Extension (MSE)

### Codec options

```javascript
const mediaCodec = 'video/mp4; codecs="avc1.4D601F"';
```

You can get the `avc1.4D601F` from using `mp4info` on a video file. This should not change unless any encoding options are changed.

## Resources

- https://developer.mozilla.org/en-US/docs/Web/API/MediaSource
- chrome://media-internals/ (for debugging MSE issues)
- https://hacks.mozilla.org/2015/07/streaming-media-on-demand-with-media-source-extensions/
- https://webplatform.github.io/docs/tutorials/MSEPrimer/
- https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API/Transcoding_assets_for_MSE
- https://www.ffmpeg.org/ffmpeg-formats.html#segment_002c-stream_005fsegment_002c-ssegment
- https://www.bento4.com/downloads/
- [`strftime` reference](http://www.cplusplus.com/reference/ctime/strftime/)
